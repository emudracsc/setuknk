<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSC डेटा डॅशबोर्ड · लाँच पेज</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            position: relative;
            overflow: hidden;
        }

        /* Animated Background */
        body::before {
            content: '';
            position: absolute;
            width: 200%;
            height: 200%;
            background: rgba(255,255,255,0.1);
            transform: rotate(45deg);
            animation: shine 10s ease-in-out infinite;
        }

        @keyframes shine {
            0% { transform: rotate(45deg) translateY(-100%); }
            100% { transform: rotate(45deg) translateY(100%); }
        }

        .container {
            max-width: 600px;
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 30px;
            padding: 50px 40px;
            box-shadow: 0 30px 60px rgba(0,0,0,0.3), 0 0 0 1px rgba(255,255,255,0.2) inset;
            text-align: center;
            position: relative;
            z-index: 10;
            animation: fadeInUp 0.8s ease;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .icon {
            width: 100px;
            height: 100px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 30px;
            box-shadow: 0 15px 30px rgba(102, 126, 234, 0.4);
        }

        .icon svg {
            width: 50px;
            height: 50px;
            fill: white;
        }

        h1 {
            font-size: 2.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 15px;
            letter-spacing: -0.5px;
        }

        .subtitle {
            font-size: 1.1rem;
            color: #4a5568;
            margin-bottom: 40px;
            line-height: 1.6;
            opacity: 0.9;
        }

        .dashboard-link {
            display: inline-block;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            text-decoration: none;
            padding: 20px 50px;
            border-radius: 60px;
            font-size: 1.3rem;
            font-weight: 600;
            letter-spacing: 1px;
            box-shadow: 0 15px 30px rgba(102, 126, 234, 0.4);
            transition: all 0.3s ease;
            margin-bottom: 30px;
            border: 2px solid rgba(255,255,255,0.3);
            position: relative;
            overflow: hidden;
        }

        .dashboard-link::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: left 0.5s ease;
        }

        .dashboard-link:hover::before {
            left: 100%;
        }

        .dashboard-link:hover {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 25px 40px rgba(102, 126, 234, 0.5);
        }

        .dashboard-link:active {
            transform: translateY(0) scale(0.98);
        }

        .features {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 40px 0 30px;
            flex-wrap: wrap;
        }

        .feature {
            text-align: center;
            flex: 1;
            min-width: 100px;
        }

        .feature-icon {
            font-size: 2rem;
            margin-bottom: 10px;
            display: block;
        }

        .feature-text {
            font-size: 0.9rem;
            color: #4a5568;
            font-weight: 500;
        }

        .instructions {
            background: #f7fafc;
            border-radius: 20px;
            padding: 25px;
            text-align: left;
            border: 1px solid #e2e8f0;
        }

        .instructions h3 {
            color: #2d3748;
            font-size: 1.2rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .instructions h3::before {
            content: '📋';
            font-size: 1.2rem;
        }

        .instructions ol {
            padding-left: 25px;
            color: #4a5568;
        }

        .instructions li {
            margin-bottom: 10px;
            line-height: 1.5;
        }

        .instructions li::marker {
            color: #667eea;
            font-weight: 600;
        }

        .note {
            margin-top: 20px;
            padding: 15px;
            background: #ebf8ff;
            border-radius: 15px;
            border-left: 4px solid #667eea;
            color: #2c5282;
            font-size: 0.95rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .note::before {
            content: '⚠️';
            font-size: 1.2rem;
        }

        .footer {
            margin-top: 30px;
            color: #718096;
            font-size: 0.9rem;
        }

        .footer a {
            color: #667eea;
            text-decoration: none;
            font-weight: 500;
        }

        .footer a:hover {
            text-decoration: underline;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                padding: 30px 20px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .dashboard-link {
                padding: 15px 30px;
                font-size: 1.1rem;
            }
            
            .features {
                gap: 15px;
            }
        }

        @media (max-width: 480px) {
            h1 {
                font-size: 1.8rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
            
            .feature-icon {
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Icon -->
        <div class="icon">
            <svg viewBox="0 0 24 24">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1 14H9V8h2v8zm4 0h-2V8h2v8z"/>
            </svg>
        </div>

        <!-- Title -->
        <h1>सेतु सुविधा केंद्र तहसील कार्यालय कणकवली</h1>
        
        <!-- Subtitle -->
        <div class="subtitle">
            तुमच्या CSC सेवांचा डेटा पाहण्यासाठी प्रीमियम डॅशबोर्ड
        </div>

        <!-- Main Link Button -->
        <a href="https://script.google.com/macros/s/AKfycbycukyycNmaplKec5L9ou5JWnpfWZ4dfepBevzkD2ot4FxrK_xv1Bh0KE-Iw3j4BVYj/exec" 
           class="dashboard-link" 
           target="_blank">
            🔗 CSC डेटा डॅशबोर्ड उघडा
        </a>

        <!-- Features -->
        <div class="features">
            <div class="feature">
                <span class="feature-icon">🌓</span>
                <span class="feature-text">Dark/Light Mode</span>
            </div>
            <div class="feature">
                <span class="feature-icon">🔍</span>
                <span class="feature-text">रिअल-टाइम शोध</span>
            </div>
            <div class="feature">
                <span class="feature-icon">📋</span>
                <span class="feature-text">कॉपी ID</span>
            </div>
            <div class="feature">
                <span class="feature-icon">📥</span>
                <span class="feature-text">PDF डाउनलोड</span>
            </div>
        </div>

        <!-- Instructions -->
        <div class="instructions">
            <h3>वापर सूचना</h3>
            <ol>
                <li>वरील बटनवर क्लिक करा</li>
                <li>Apps Script ला परवानगी द्या (पहिल्यांदाच)</li>
                <li>डॅशबोर्ड उघडेल</li>
                <li>नाव किंवा ID ने शोधा</li>
                <li>PDF डाउनलोड करा</li>
            </ol>
        </div>

        <!-- Note -->
        <div class="note">
            पहिल्यांदा उघडताना परवानगी मागेल, कृपया Allow करा
        </div>

        <!-- Footer -->
        <div class="footer">
            <p>⚡ प्रीमियम CSC डेटा डॅशबोर्ड ⚡</p>
            <p style="margin-top: 10px; font-size: 0.8rem;">
                <a href="https://github.com" target="_blank">GitHub</a> · 
                <a href="#" onclick="window.location.reload()">Refresh</a>
            </p>
        </div>
    </div>
</body>
</html>
