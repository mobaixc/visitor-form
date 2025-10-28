<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>访客登记系统</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 20px; }
        .container { background: white; border-radius: 20px; box-shadow: 0 20px 40px rgba(0,0,0,0.1); padding: 40px; max-width: 500px; width: 100%; }
        h1 { text-align: center; color: #333; margin-bottom: 30px; font-size: 28px; }
        .form-group { margin-bottom: 20px; }
        label { display: block; margin-bottom: 8px; color: #555; font-weight: 500; }
        input, select, textarea { width: 100%; padding: 12px 16px; border: 2px solid #e1e5e9; border-radius: 10px; font-size: 16px; transition: border-color 0.3s; }
        input:focus, select:focus, textarea:focus { outline: none; border-color: #667eea; }
        .radio-group { display: flex; gap: 20px; margin-top: 8px; }
        .radio-option { display: flex; align-items: center; gap: 8px; }
        .radio-option input[type="radio"] { width: auto; }
        .submit-btn { width: 100%; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border: none; padding: 16px; border-radius: 10px; font-size: 18px; font-weight: 600; cursor: pointer; transition: transform 0.2s; }
        .submit-btn:hover { transform: translateY(-2px); }
        .success-message { display: none; background: #d4edda; color: #155724; padding: 16px; border-radius: 10px; margin-top: 20px; text-align: center; }
        .loading { display: none; text-align: center; margin-top: 20px; color: #667eea; }
    </style>
</head>
<body>
    <div class="container">
        <h1>访客登记</h1>
        <form id="visitorForm">
            <div class="form-group">
                <label for="visitorName">访客姓名 *</label>
                <input type="text" id="visitorName" name="访客姓名" required>
            </div>
            
            <div class="form-group">
                <label for="phone">联系电话 *</label>
                <input type="tel" id="phone" name="联系电话" required>
            </div>
            
            <div class="form-group">
                <label>是否面试人员 *</label>
                <div class="radio-group">
                    <div class="radio-option">
                        <input type="radio" id="interviewYes" name="是否面试人员" value="是" required>
                        <label for="interviewYes">是</label>
                    </div>
                    <div class="radio-option">
                        <input type="radio" id="interviewNo" name="是否面试人员" value="否" required>
                        <label for="interviewNo">否</label>
                    </div>
                </div>
            </div>
            
            <div class="form-group" id="purposeGroup" style="display: none;">
                <label for="purpose">访问目的 *</label>
                <input type="text" id="purpose" name="访问目的">
            </div>
            
            <div class="form-group" id="positionGroup" style="display: none;">
                <label for="position">面试岗位</label>
                <input type="text" id="position" name="面试岗位">
            </div>
            
            <div class="form-group">
                <label for="visitTime">访问时间 *</label>
                <input type="datetime-local" id="visitTime" name="访问时间" required>
            </div>
            
            <button type="submit" class="submit-btn">提交登记</button>
        </form>
        
        <div class="loading" id="loading">正在提交...</div>
        <div class="success-message" id="successMessage">
            登记成功！感谢您的配合。
        </div>
    </div>

    <script>
        // 显示/隐藏访问目的和面试岗位字段
        document.querySelectorAll('input[name="是否面试人员"]').forEach(radio
