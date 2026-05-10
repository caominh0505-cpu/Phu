# Phu
script dành cho anh em
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Phú Doors V1 | Script Hub - Sao chép & Sử dụng</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #0a0f1e 0%, #0c1222 100%);
            font-family: 'Segoe UI', 'Poppins', 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Roboto', sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem 1rem;
        }

        /* container chính */
        .glass-card {
            max-width: 1100px;
            width: 100%;
            background: rgba(18, 22, 35, 0.85);
            backdrop-filter: blur(12px);
            border-radius: 2rem;
            border: 1px solid rgba(255, 215, 0, 0.25);
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(255, 215, 0, 0.1) inset;
            overflow: hidden;
            transition: all 0.2s ease;
        }

        /* header */
        .header {
            background: rgba(0, 0, 0, 0.5);
            padding: 1.2rem 1.8rem;
            border-bottom: 1px solid rgba(255, 215, 0, 0.4);
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: baseline;
            gap: 0.8rem;
        }

        .title-section h1 {
            color: #FFD966;
            font-size: 1.8rem;
            letter-spacing: -0.5px;
            font-weight: 700;
            background: linear-gradient(135deg, #FFE484, #FFB347);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }

        .title-section p {
            color: #9aa4bf;
            font-size: 0.85rem;
            margin-top: 0.3rem;
            display: flex;
            align-items: center;
            gap: 0.4rem;
        }

        .badge {
            background: #1e2a3e;
            border-radius: 40px;
            padding: 0.2rem 0.8rem;
            font-size: 0.7rem;
            font-weight: 500;
            color: #ffd966;
            border: 1px solid #ffd96640;
        }

        .info-badge {
            background: #0f172a;
            color: #b9c7ff;
        }

        /* nút copy chính */
        .copy-btn {
            background: linear-gradient(95deg, #2a2f3f, #1e2436);
            border: none;
            padding: 0.7rem 1.4rem;
            border-radius: 2rem;
            font-weight: 600;
            font-size: 0.9rem;
            color: #ece9e0;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
            display: inline-flex;
            align-items: center;
            gap: 8px;
            border: 1px solid rgba(255,215,0,0.4);
        }

        .copy-btn i {
            font-size: 1.1rem;
            font-style: normal;
            font-weight: bold;
        }

        .copy-btn:hover {
            background: linear-gradient(95deg, #3a4055, #2b3148);
            transform: translateY(-2px);
            box-shadow: 0 12px 22px rgba(0, 0, 0, 0.4);
            border-color: #ffd966;
            color: #ffeaac;
        }

        .copy-btn:active {
            transform: translateY(1px);
        }

        /* thông báo toast */
        .toast-msg {
            position: fixed;
            bottom: 25px;
            left: 50%;
            transform: translateX(-50%) scale(0.9);
            background: #1f2a3ecc;
            backdrop-filter: blur(20px);
            color: #ccffcc;
            padding: 12px 24px;
            border-radius: 60px;
            font-size: 0.9rem;
            font-weight: 500;
            border-left: 4px solid #66ff66;
            border-right: 4px solid #66ff66;
            box-shadow: 0 8px 20px black;
            opacity: 0;
            transition: opacity 0.2s, transform 0.2s;
            pointer-events: none;
            z-index: 999;
            font-family: monospace;
            backdrop-filter: blur(12px);
        }

        .toast-msg.show {
            opacity: 1;
            transform: translateX(-50%) scale(1);
        }

        /* code wrapper */
        .code-container {
            padding: 1.5rem 1.8rem;
        }

        .code-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            border-bottom: 1px dashed #2a3348;
            padding-bottom: 0.5rem;
        }

        .code-header span {
            font-family: 'Fira Code', 'JetBrains Mono', monospace;
            background: #0f111c;
            padding: 0.2rem 0.8rem;
            border-radius: 20px;
            font-size: 0.75rem;
            color: #cbd5ff;
            letter-spacing: 0.3px;
        }

        .copy-mini {
            background: none;
            border: none;
            color: #b9c7ff;
            cursor: pointer;
            font-size: 0.75rem;
            padding: 4px 10px;
            border-radius: 30px;
            transition: 0.2s;
            font-weight: 500;
        }

        .copy-mini:hover {
            background: #2f3b54;
            color: #ffd966;
        }

        pre {
            background: #0b0e16e6;
            border-radius: 1.2rem;
            padding: 1.2rem;
            overflow-x: auto;
            white-space: pre-wrap;
            word-wrap: break-word;
            font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
            font-size: 0.85rem;
            line-height: 1.5;
            color: #e2e8ff;
            border: 1px solid #2e3a4e;
            box-shadow: inset 0 0 12px rgba(0,0,0,0.4), 0 6px 12px rgba(0,0,0,0.2);
            max-height: 65vh;
            overflow-y: auto;
        }

        code {
            font-family: inherit;
        }

        /* hướng dẫn sử dụng */
        .usage {
            background: rgba(0, 0, 0, 0.3);
            margin: 0 1.8rem 1.5rem 1.8rem;
            padding: 1rem 1.4rem;
            border-radius: 1.5rem;
            font-size: 0.8rem;
            border-left: 3px solid #ffd966;
            color: #bec8e6;
            backdrop-filter: blur(4px);
        }

        .usage strong {
            color: #ffd966;
        }

        hr {
            border-color: #2a334a;
            margin: 0 1.8rem 1rem;
        }

        footer {
            text-align: center;
            padding: 1rem;
            font-size: 0.7rem;
            color: #5f6c8a;
            border-top: 1px solid #1e253b;
        }

        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #10131f;
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb {
            background: #ffd96680;
            border-radius: 10px;
        }

        @media (max-width: 650px) {
            .header {
                flex-direction: column;
                align-items: flex-start;
            }
            .code-container {
                padding: 1rem;
            }
            .usage {
                margin: 0 1rem 1.2rem 1rem;
            }
            pre {
                font-size: 0.75rem;
                padding: 0.8rem;
            }
            .title-section h1 {
                font-size: 1.4rem;
            }
        }
    </style>
</head>
<body>
<div class="glass-card">
    <div class="header">
        <div class="title-section">
            <h1>⚡ PHÚ DOORS V1</h1>
            <p><span class="badge">✨ ESP + TỰ ĐỘNG MỞ CỬA</span> 
            <span class="badge info-badge">🔆 NHÌN TRONG TỐI</span>
            <span class="badge info-badge">🎨 NÚT BẬT/TẮT MÀU XANH</span></p>
        </div>
        <button class="copy-btn" id="globalCopyBtn">
            <i>📋</i> Sao chép toàn bộ script
        </button>
    </div>

    <div class="code-container">
        <div class="code-header">
            <span>📜 script.lua – Phú Doors V1 (cập nhật màu nút & Bật/Tắt)</span>
            <button class="copy-mini" id="miniCopyBtn">📄 sao chép code</button>
        </div>
        <pre id="scriptCode"><code>-- Script: Phú Doors V1 (Cập nhật màu nút & Bật/Tắt)
-- Tác giả: phu-dep-trai

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local NotifyGui = Instance.new("ScreenGui")

ScreenGui.Parent = game.CoreGui
NotifyGui.Parent = game.CoreGui
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.Size = UDim2.new(0, 220, 0, 200) -- Thu gọn vì đã xoá nút thoát
MainFrame.Position = UDim2.new(0.1, 0, 0.2, 0)
MainFrame.Active = true
MainFrame.Draggable = true

Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "Phú Doors V1"
Title.TextColor3 = Color3.fromRGB(255, 215, 0)
Title.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Title.TextSize = 18
Title.Font = Enum.Font.SourceSansBold

-- Hàm thông báo quái vật
local function NotifyMonster(msg)
    local label = Instance.new("TextLabel", NotifyGui)
    label.Size = UDim2.new(0, 180, 0, 40)
    label.Position = UDim2.new(1, -200, 0.1, 0)
    label.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    label.Text = "⚠️ " .. msg
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextSize = 12
    label.Font = Enum.Font.SourceSansBold
    task.delay(4, function() label:Destroy() end)
end

-- ESP Chữ nhỏ + Số mét
local function CreateMiniESP(part, text, color)
    if part:FindFirstChild("PhuTagV1") then part.PhuTagV1:Destroy() end
    local bill = Instance.new("BillboardGui", part)
    bill.Name = "PhuTagV1"
    bill.AlwaysOnTop = true
    bill.Size = UDim2.new(0, 60, 0, 20)
    bill.Adornee = part
    bill.MaxDistance = 250
    local label = Instance.new("TextLabel", bill)
    label.BackgroundTransparency = 1
    label.Size = UDim2.new(1, 0, 1, 0)
    label.TextColor3 = color
    label.TextSize = 10
    label.Font = Enum.Font.SourceSansBold
    task.spawn(function()
        while bill and bill.Parent do
            local char = game.Players.LocalPlayer.Character
            if char and char:FindFirstChild("HumanoidRootPart") then
                local dist = math.floor((char.HumanoidRootPart.Position - part.Position).Magnitude)
                label.Text = text .. " [" .. dist .. "m]"
            end
            task.wait(0.5)
        end
    end)
end

-- Biến trạng thái
local espOn = false
local autoOn = false
local lightOn = false

-- Hàm tạo nút đổi màu
local function AddToggleBtn(text, pos, callback)
    local btn = Instance.new("TextButton", MainFrame)
    btn.Size = UDim2.new(0, 200, 0, 40)
    btn.Position = pos
    btn.Text = text
    btn.BackgroundColor3 = Color3.fromRGB(100, 100, 100) -- Mặc định màu xám (Tắt)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.SourceSansBold
    
    local active = false
    btn.MouseButton1Click:Connect(function()
        active = not active
        if active then
            btn.BackgroundColor3 = Color3.fromRGB(0, 120, 255) -- Màu xanh dương (Bật)
        else
            btn.BackgroundColor3 = Color3.fromRGB(100, 100, 100) -- Màu xám (Tắt)
        end
        callback(active)
    end)
end

-- Nút ESP
AddToggleBtn("ESP + MÉT (VIỆT HÓA)", UDim2.new(0, 10, 0, 50), function(state)
    espOn = state
    task.spawn(function()
        while espOn do
            for _, v in pairs(workspace:GetDescendants()) do
                if v.Name == "RushNew" or v.Name == "Ambush" then
                    if not v:FindFirstChild("Warned") then NotifyMonster("CÓ QUÁI VẬT!") local w = Instance.new("BoolValue", v) w.Name = "Warned" end
                    CreateMiniESP(v:IsA("Model") and v.PrimaryPart or v, "QUÁI", Color3.fromRGB(255, 0, 0))
                elseif v.Name == "Key" or v.Name == "LibraryKey" then
                    CreateMiniESP(v, "CHÌA KHÓA", Color3.fromRGB(255, 255, 0))
                elseif v.Name == "Door" and v:FindFirstChild("Door") then
                    CreateMiniESP(v.Door, "CỬA", Color3.fromRGB(0, 255, 0))
                end
            end
            task.wait(1.5)
        end
        -- Xoá ESP khi tắt
        for _, v in pairs(workspace:GetDescendants()) do if v.Name == "PhuTagV1" then v:Destroy() end end
    end)
end)

-- Nút Auto Cửa
AddToggleBtn("AUTO MỞ CỬA", UDim2.new(0, 10, 0, 100), function(state)
    autoOn = state
    task.spawn(function()
        while autoOn do
            local char = game.Players.LocalPlayer.Character
            if char and char:FindFirstChild("HumanoidRootPart") then
                for _, v in pairs(workspace:GetDescendants()) do
                    if v:IsA("ProximityPrompt") and (v.Parent.Name == "Door" or v.Parent.Name == "Knob") then
                        if (char.HumanoidRootPart.Position - v.Parent.Position).Magnitude < 12 then fireproximityprompt(v) end
                    end
                end
            end
            task.wait(0.1)
        end
    end)
end)

-- Nút Nhìn Tối
AddToggleBtn("NHÌN TRONG BÓNG TỐI", UDim2.new(0, 10, 0, 150), function(state)
    lightOn = state
    local Lighting = game:GetService("Lighting")
    if lightOn then
        Lighting.Brightness = 2
        Lighting.ClockTime = 14
        Lighting.OutdoorAmbient = Color3.fromRGB(255, 255, 255)
    else
        Lighting.Brightness = 1 -- Trả về mặc định
        Lighting.ClockTime = 0
        Lighting.OutdoorAmbient = Color3.fromRGB(0, 0, 0)
    end
end)
</code></pre>
    </div>

    <div class="usage">
        <strong>📌 HƯỚNG DẪN SỬ DỤNG:</strong> <br>
        • Sao chép toàn bộ script ở trên → Mở Roblox, chạy executor (như Synapse, Krnl, Fluxus...).<br>
        • Dán script và thực thi (Execute). <br>
        • Giao diện sẽ xuất hiện kéo thả được, các nút chức năng <span style="color:#ffd966;">ESP + mét (hiện quái, chìa khóa, cửa)</span>, 
        <span style="color:#ffd966;">Auto mở cửa</span> và <span style="color:#ffd966;">Nhìn trong bóng tối</span>.<br>
        • Mỗi khi bật, nút chuyển sang <strong style="color:#3b82f6;">màu xanh dương</strong> – tắt trở về xám.<br>
        • Được tối ưu cho game <strong>DOORS</strong>, hiển thị cả khoảng cách (mét) và cảnh báo quái vật.<br>
        ➤ Tác giả: <strong>phu-dep-trai</strong> – bản cập nhật mới nhất.
    </div>
    <hr />
    <footer>
        ⚡ Phú Doors V1 · Sao chép miễn phí · Hỗ trợ hầu hết Roblox Executor
    </footer>
</div>

<div id="toastMsg" class="toast-msg">✅ Đã sao chép script vào clipboard!</div>

<script>
    (function() {
        // lấy nội dung code từ thẻ pre (đảm bảo lấy chính xác)
        const preElement = document.getElementById('scriptCode');
        let fullScriptText = '';
        if (preElement) {
            // Lấy text bên trong (có thể bao gồm thẻ code nhưng .innerText giữ nguyên dòng)
            const codeElement = preElement.querySelector('code');
            if (codeElement) {
                fullScriptText = codeElement.innerText;
            } else {
                fullScriptText = preElement.innerText;
            }
        } else {
            // fallback cứng
            fullScriptText = `-- Script: Phú Doors V1 (Cập nhật màu nút & Bật/Tắt)\n-- Tác giả: phu-dep-trai\n\nlocal ScreenGui = Instance.new("ScreenGui")\n--...`; 
        }

        // hàm hiện toast
        function showToast(message) {
            let toast = document.getElementById('toastMsg');
            if (!toast) {
                toast = document.createElement('div');
                toast.id = 'toastMsg';
                toast.className = 'toast-msg';
                document.body.appendChild(toast);
            }
            toast.textContent = message || '✅ Đã sao chép script vào clipboard!';
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 2200);
        }

        // copy text vào clipboard
        async function copyToClipboard(textToCopy, successMsg = "✅ Đã sao chép script!") {
            if (!textToCopy) {
                showToast("⚠️ Không có nội dung để sao chép");
                return false;
            }
            try {
                await navigator.clipboard.writeText(textToCopy);
                showToast(successMsg);
                return true;
            } catch (err) {
                // fallback dùng textarea
                const textarea = document.createElement('textarea');
                textarea.value = textToCopy;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                showToast(successMsg);
                return true;
            }
        }

        // nút copy toàn bộ (global)
        const globalBtn = document.getElementById('globalCopyBtn');
        if (globalBtn) {
            globalBtn.addEventListener('click', () => {
                copyToClipboard(fullScriptText, "📋 Đã sao chép toàn bộ script Phú Doors V1!");
            });
        }

        // nút copy mini trong header code
        const miniBtn = document.getElementById('miniCopyBtn');
        if (miniBtn) {
            miniBtn.addEventListener('click', () => {
                copyToClipboard(fullScriptText, "📄 Code đã được sao chép!");
            });
        }

        // đảm bảo script text được lấy chính xác nếu có sự thay đổi DOM (không cần nhưng dự phòng)
        const updateRawScript = () => {
            const freshPre = document.getElementById('scriptCode');
            if (freshPre) {
                const freshCode = freshPre.querySelector('code');
                if (freshCode) {
                    fullScriptText = freshCode.innerText;
                } else {
                    fullScriptText = freshPre.innerText;
                }
            }
        };
        // chạy 1 lần nữa để đồng bộ
        updateRawScript();
    })();
</script>
</body>
</html>
