<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WWW(スリーダブリュー) BAR イベント情報（予約システム）</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Hiragino Sans', 'Hiragino Kaku Gothic ProN', 'Yu Gothic', sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
            background-image: linear-gradient(rgba(255,255,255,0.9), rgba(255,255,255,0.9)), 
                              url('C:/pleiades/2025-09/workspace/wwwbar/src/main/webapp/images/background.jpg');
            background-size: cover;
            background-attachment: fixed;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background-color: rgba(44, 62, 80, 0.9);
            color: white;
            padding: 15px 0;
            text-align: center;
            margin-bottom: 30px;
            border-radius: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }
        
        .logo {
            height: 120px;
            width: auto;
        }
        
        .user-info {
            background-color: rgba(52, 152, 219, 0.9);
            color: white;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 30px;
            text-align: right;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .user-avatar {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            border: 2px solid white;
        }
        
        .events-container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin-bottom: 40px;
        }
        
        .event-card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 20px;
            flex: 1;
            min-width: 300px;
            transition: transform 0.3s ease;
        }
        
        .event-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
        }
        
        .event-image {
            width: 100%;
            height: 180px;
            object-fit: cover;
            border-radius: 5px;
            margin-bottom: 15px;
        }
        
        .event-date {
            font-weight: bold;
            font-size: 1.2em;
            margin-bottom: 10px;
            color: #2c3e50;
            border-bottom: 2px solid #e74c3c;
            padding-bottom: 5px;
        }
        
        .event-time {
            color: #7f8c8d;
            margin-bottom: 10px;
        }
        
        .event-title {
            font-size: 1.3em;
            font-weight: bold;
            margin-bottom: 10px;
            color: #2c3e50;
            min-height: 60px;
        }
        
        .event-details {
            margin-bottom: 15px;
        }
        
        .capacity-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        
        .capacity-bar {
            height: 10px;
            background-color: #ecf0f1;
            border-radius: 5px;
            margin-bottom: 15px;
            overflow: hidden;
        }
        
        .capacity-fill {
            height: 100%;
            background-color: #2ecc71;
        }
        
        .action-buttons {
            display: flex;
            gap: 10px;
        }
        
        .btn {
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            flex: 1;
            text-align: center;
            transition: all 0.3s ease;
        }
        
        .btn-join {
            background-color: #2ecc71;
            color: white;
        }
        
        .btn-join:hover {
            background-color: #27ae60;
        }
        
        .btn-cancel {
            background-color: #e74c3c;
            color: white;
        }
        
        .btn-cancel:hover {
            background-color: #c0392b;
        }
        
        .shop-info {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-top: 30px;
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            align-items: center;
        }
        
        .shop-details {
            flex: 1;
            min-width: 300px;
        }
        
        .shop-info h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            border-bottom: 2px solid #e74c3c;
            padding-bottom: 5px;
        }
        
        .map-image {
            flex: 1;
            min-width: 300px;
            height: 200px;
            border-radius: 5px;
            overflow: hidden;
        }
        
        .map-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        footer {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            color: #7f8c8d;
            font-size: 0.9em;
        }
        
        @media (max-width: 768px) {
            .events-container {
                flex-direction: column;
            }
            
            .user-info {
                flex-direction: column;
                text-align: center;
                gap: 10px;
            }
            
            .shop-info {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <img src="https://msp.c.yimg.jp/images/v2/FUTi93tXq405grZVGgDqG7s6XIz6WzUM9mMsixYxaAvYvygdbrnEqsjbkPRrTAsNDdKJyRaybHddVpn8eXWx4lVzIsMp8eaYHcH-asWp53Oo0DqYNacpvNnC_8I53xe6O5veJ9kVV9EUknhX13bq02LzN-9yItHMsHvWQnhPeNHA6QPJwkzXYf0MBiSIyVHoMgDdwiqqwimpKBpo8VBNnEAmPE1PxfN-H7d331Vgvnw6bHkxjLlRZ4PiXnlIX6moHI6h6Vior_h1kzk19VLb_YZQuGT2-odDB9Odaxaz_zNC92xUMn3_hSuQRBww4ONwqZXm079QiJuZsz9SiYRSLvrvtfMPbq4lj85-N1GYRyI0yUbdzx1VDGfasBNAbE8zT6JUmODU-eQAPiwE4VnZnpt7yXWQpNrHVw-JifQB4chYg-o8AjVTaEciyub9pKXS_v8Ybtkps2h6yuWVmAz6h-iG-BcUWvyHgE-GfE2SPJJh64464LZ3HZKfznWOrTxV02YrC7zV-6fKVDORn82pVctEY04IAUXQ3ZrvJD7JflAKiNBf2INoTcp51-pICohVD-eHyW4cWoooW6UoROkALYwQUr2uPRjssvIKp0lzNh5caPRnczZZkhb6Ym94bf9_VgYWEfpGpML-rV4VGTkkjS-v_qv4_yJesJY1YGK-6K0SzCmktOvxrTLDIJYPZqDl3WpFkrrAtyh58vDqIPO1QQoI31JlwJMPvi0X8xjSl4MUjL33lsYFzC5aNgdNf8nj/E382A2E383ABE382B3E383BCE383ABE9A3B2E69699E381A8E38390E383BCE382ABE382A6E383B3E382BFE383BC.jpg" alt="WWW BAR ロゴ" class="logo">
            <h1>WWW(スリーダブリュー) BAR イベント情報（予約システム）</h1>
        </header>
        
        <div class="user-info">
            <div>
                <p>ユーザーID：AF2025 | ユーザー名：やまちゃん | 性別：男</p>
                <p>(ユーザー情報変更不可)</p>
            </div>
            <img src="https://msp.c.yimg.jp/images/v2/FUTi93tXq405grZVGgDqG9Q4Ibdn-_OFi1gO8mqkJyv6nrFeQZgeeb_jlQ_jkkHoBFSPyXP5bjeTGtLp4Q6FA4ANWtGqLZJYethmNhOb7L3SQHfYYQGgiD08qD9ZSTRqp6sM-6car1btiqJFAYi06KfX2v5kiEaU4P-jPPu-Ypp0udcRLHaL6MVtChWm8aigAiWmmLR3v7pkRaq-ebFYSckuf9MsijgRI-YNzwctj_LVIxKttHGK-mp63yHW8Cl9x-A9dzEPGFNgRIWeZi9SPP6V24Z7bASD9ZmLR7jL4gxSV_x8IEtsj3gYcZPsaCmT5hRjcs7_7psJlWdPjQyfioThMa_xHh5XgHWeOMs-YgM=/6f9296be.png?errorImage=false" alt="ユーザーアバター" class="user-avatar">
        </div>
        
        <div class="events-container">
            <!-- 12月22日 月曜日 イベント -->
            <div class="event-card">
                <img src="https://msp.c.yimg.jp/images/v2/FUTi93tXq405grZVGgDqG55TuUok74aGR5j448WXX6SoNxlrqvrEYnNXozCrzKMxIZWLRtSgRhDQeMwfG4ncKaztxpJ5481V-5GFtXm_fct3RdGC9LV2RTOxOnXIMwAsffqNrfTLZwZRJ9cgBYOIGnR02-1PTDQCOP0IF86YTxitc25WAa412dy59vRYJEGH4zFDTRHbf2SKV0b5GMz0FX6x1u7PE3hFj1tQl9OenK0=/d1355-1445-187212-0.jpg?errorImage=false" alt="B'Zイベント" class="event-image">
                <div class="event-date">12月22日 月曜日</div>
                <div class="event-time">20:00:00-22:00</div>
                <div class="event-title">B'Zが好きな人集まろう！</div>
                <div class="event-details">
                    <p>参加費：3000円 飲み放題軽食つき</p>
                    <div class="capacity-info">
                        <span>定員：10名</span>
                        <span>空き：4名</span>
                    </div>
                    <div class="capacity-info">
                        <span>現在男性：3名</span>
                        <span>現在女性：3名</span>
                    </div>
                    <div class="capacity-bar">
                        <div class="capacity-fill" style="width: 60%"></div>
                    </div>
                </div>
                <div class="action-buttons">
                    <button class="btn btn-join">参加</button>
                    <button class="btn btn-cancel">取り消し</button>
                </div>
            </div>
            
            <!-- 12月23日 火曜日 イベント -->
            <div class="event-card">
                <img src="https://msp.c.yimg.jp/images/v2/FUTi93tXq405grZVGgDqGyT8LYFcthQDA-DS2mkMeIkOxsaovFp0WhdR0EUoZgtAkwzoqwZ9btAQTGv4F_1rga-2vh7KPgdCdjVioLOjIVG0wf0WpgX02qhUuqrmUhIxhe4BVdH97elDyzegcqkyVIbn071Klx_EkihzmwC1EtiN2X5ONwygLwrKDGCqVac9LAHD5JCjpiUOTODuec_HAUqziG--IQu9-QD00MHIee-5yBl7y-V295AXd9OmbSTfCHT4POPSzuaXzIUQYTX30hvs9rtq1-aVB-qgnVnjuIaty8qqFopJV8Ldf-_4CXD4UoT23BitlKzOwpYuCCVBKWwmoPMHiUHDuGstSF0lcME=/topimg_original.jpg" alt="人狼ゲームイベント" class="event-image">
                <div class="event-date">12月23日 火曜日</div>
                <div class="event-time">20:00:00-22:00</div>
                <div class="event-title">人狼ゲームをやりましょう！</div>
                <div class="event-details">
                    <p>参加費：3000円 飲み放題軽食つき</p>
                    <div class="capacity-info">
                        <span>定員：15名</span>
                        <span>空き：6名</span>
                    </div>
                    <div class="capacity-info">
                        <span>現在男性：5名</span>
                        <span>現在女性：3名</span>
                    </div>
                    <div class="capacity-bar">
                        <div class="capacity-fill" style="width: 53%"></div>
                    </div>
                </div>
                <div class="action-buttons">
                    <button class="btn btn-join">参加</button>
                    <button class="btn btn-cancel">取り消し</button>
                </div>
            </div>
            
            <!-- 12月24日 火曜日 イベント -->
            <div class="event-card">
                <img src="https://msp.c.yimg.jp/images/v2/FUTi93tXq405grZVGgDqGxx454imGcRwjmoexk8Nh1pZ6I_Xy3B0fGs_kv7En1k5H0QUnqndppz4gWgRwiTg7l5AIkF5ufravNJxcETSXVQyZnNEdiOtYSGUogUc1FfvMro5GnM9_s4WkPjSf8zf7MtHIBNcBJSWnjXMENmNoOSgbRX6Bp_QkuQQiqOBYDk5y8PKpHShYEMNUIqpLOqxMHNTvXg7ZgFkl6v8LDGxjPdYF072B_AzNpYJicAQTTMx8o6zQcPYl1uIAxkvjQDVUg==/95367302.jpg" alt="クリスマスイベント" class="event-image">
                <div class="event-date">12月24日 火曜日</div>
                <div class="event-time">20:00:00-22:00</div>
                <div class="event-title">クリスマスイブ合コン</div>
                <div class="event-details">
                    <p>参加費：4000円 飲み放題イタリア料理</p>
                    <div class="capacity-info">
                        <span>定員：12名</span>
                        <span>空き：3名</span>
                    </div>
                    <div class="capacity-info">
                        <span>現在男性：6名 (男性上限6)</span>
                        <span>現在女性：3名 (女性上限6)</span>
                    </div>
                    <div class="capacity-bar">
                        <div class="capacity-fill" style="width: 75%"></div>
                    </div>
                </div>
                <div class="action-buttons">
                    <button class="btn btn-join">参加</button>
                    <button class="btn btn-cancel">取り消し</button>
                </div>
            </div>
        </div>
        
        <div class="shop-info">
            <div class="shop-details">
                <h3>店舗情報</h3>
                <p>住所：800-0000 福岡市天神0-0-0</p>
                <p>営業時間：18：00-24：00</p>
                <p>電話番号：092-0000-000</p>
            </div>
            <div class="map-image">
                <img src="https://msp.c.yimg.jp/images/v2/FUTi93tXq405grZVGgDqG7st3QcFCUNtxtLKK0qbyKb-MVQ-EIn9n4AYfaFYKagijIWe_6T1Es_LoJGctuQsDIFW21zOm0eQaXQygRJpli_szzCbZENTza-YgU3U-_hF34UB92K95BecaCOrNt7dgFRhkenkClH7Pi5OOxpeL2AGQ9YviTsqbfW9Gmu_pZC0ubTXUxpYKQpuS7zrwbK0E2C2QC1lJeEldkvH8SAjrMA=/image.png?errorImage=false" alt="店舗地図">
            </div>
        </div>
        
        <footer>
            <p>© 2023 WWW(スリーダブリュー) BAR イベント情報</p>
        </footer>
    </div>
</body>
</html>
