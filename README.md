



<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>SLR | Ban Appeal</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #0f172a;
            color: #e5e7eb;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }
        .container {
            background-color: #111827;
            padding: 20px 24px;
            border-radius: 8px;
            max-width: 500px;
            width: 100%;
            box-shadow: 0 10px 25px rgba(0,0,0,0.6);
        }
        h1 {
            font-size: 1.4rem;
            margin-bottom: 16px;
            text-align: center;
        }
        .form-group {
            margin-bottom: 12px;
        }
        label {
            display: block;
            font-size: 0.9rem;
            margin-bottom: 4px;
        }
        input[type="text"],
        textarea {
            width: 100%;
            padding: 8px 10px;
            border-radius: 4px;
            border: 1px solid #374151;
            background-color: #1f2937;
            color: #e5e7eb;
            font-size: 0.9rem;
        }
        textarea {
            resize: vertical;
            min-height: 80px;
        }
        input:focus,
        textarea:focus {
            outline: none;
            border-color: #3b82f6;
        }
        button {
            width: 100%;
            padding: 10px;
            border-radius: 4px;
            border: none;
            background-color: #3b82f6;
            color: #f9fafb;
            font-size: 0.95rem;
            cursor: pointer;
            margin-top: 8px;
        }
        button:hover {
            background-color: #2563eb;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>SLR | Ban Appeal</h1>

        <form id="appealForm">
            <div class="form-group">
                <label>Discord User:</label>
                <input type="text" id="discordUser" required>
            </div>

            <div class="form-group">
                <label>Discord ID:</label>
                <input type="text" id="discordId" required>
            </div>

            <div class="form-group">
                <label>Roblox User:</label>
                <input type="text" id="robloxUser" required>
            </div>

            <div class="form-group">
                <label>Roblox ID:</label>
                <input type="text" id="robloxId" required>
            </div>

            <div class="form-group">
                <label>Reason for Ban:</label>
                <input type="text" id="reasonBan" required>
            </div>

            <div class="form-group">
                <label>Case ID (Short):</label>
                <input type="text" id="caseIdShort" placeholder="e.g. 2039-A">
            </div>

            <div class="form-group">
                <label>Case ID Full Number / Letter ID:</label>
                <input type="text" id="caseIdFull" placeholder="e.g. SLR-2039-A-XL-4920">
            </div>

            <div class="form-group">
                <label>Why should we unban you?</label>
                <textarea id="whyUnban" required></textarea>
            </div>

            <button type="submit">Submit Appeal</button>
        </form>
    </div>

<script>
document.getElementById("appealForm").addEventListener("submit", function(e) {
    e.preventDefault();

    const webhook = "https://discord.com/api/webhooks/1520990266339754146/cJjPciu4-OfEOhSMdOUXiUwU3MHJcj0b696UB3neHpjBdV8PxVbSXQVzvMFKEVYPysqv";

    // -----------------------------
    // AI DECISION ENGINE (SIMULATED)
    // -----------------------------
    let appealText = document.getElementById("whyUnban").value.toLowerCase();
    let score = 0;

    const positiveKeywords = ["sorry", "apologise", "apology", "improve", "promise", "won't happen", "won’t happen", "changed", "change"];
    const negativeKeywords = ["staff abuse", "exploiting", "ddos", "threat", "alt", "ban evasion"];

    positiveKeywords.forEach(word => { if (appealText.includes(word)) score += 2; });
    negativeKeywords.forEach(word => { if (appealText.includes(word)) score -= 3; });

    let verdict = "";
    let reasoning = "";

    if (score >= 3) {
        verdict = "ACCEPT";
        reasoning = "The automated evaluation system detected strong indicators of remorse, accountability, and willingness to comply with community rules.";
    } else if (score <= -1) {
        verdict = "DECLINE";
        reasoning = "The system detected high‑risk behavioural indicators, including terms associated with severe rule violations or ban‑evasion patterns.";
    } else {
        verdict = "REVIEW REQUIRED";
        reasoning = "The system could not confidently determine intent. Manual staff review is recommended.";
    }

    // -----------------------------
    // DISCORD EMBED PAYLOAD
    // -----------------------------
    const payload = {
        username: "SLR Automated Ban Appeals",
        avatar_url: "https://i.imgur.com/4M34hi2.png",
        embeds: [
            {
                title: "SLR Ban Appeal – New Submission",
                color: verdict === "ACCEPT" ? 5763719 : verdict === "DECLINE" ? 15548997 : 16776960,
                description: "**Automated AI Evaluation Completed**\nBelow is the full appeal and system‑generated decision.",
                fields: [
                    { name: "Discord User", value: document.getElementById("discordUser").value },
                    { name: "Discord ID", value: document.getElementById("discordId").value },
                    { name: "Roblox User", value: document.getElementById("robloxUser").value },
                    { name: "Roblox ID", value: document.getElementById("robloxId").value },
                    { name: "Reason for Ban", value: document.getElementById("reasonBan").value },
                    { name: "Case ID (Short)", value: document.getElementById("caseIdShort").value || "Not Provided" },
                    { name: "Case ID Full Number / Letter ID", value: document.getElementById("caseIdFull").value || "Not Provided" },
                    { name: "Appeal Statement", value: document.getElementById("whyUnban").value },
                    { name: "AI Verdict", value: verdict },
                    { name: "AI Reasoning Summary", value: reasoning }
                ],
                footer: {
                    text: "SLR Automated Appeal System • Intelligent Review Module v3.2"
                },
                timestamp: new Date().toISOString()
            }
        ]
    };

    fetch(webhook, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload)
    })
    .then(() => alert("Your appeal has been submitted."))
    .catch(() => alert("Error sending appeal."));
});
</script>

</body>
</html>
