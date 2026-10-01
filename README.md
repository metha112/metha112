<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Profile README Generator</title>

    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }

        body {
            background: #0d1117;
            color: #c9d1d9;
            min-height: 100vh;
        }

        header {
            text-align: center;
            padding: 35px 20px;
            border-bottom: 1px solid #30363d;
        }

        header h1 {
            color: #58a6ff;
            font-size: 32px;
            margin-bottom: 10px;
        }

        header p {
            color: #8b949e;
        }

        .container {
            width: 90%;
            max-width: 1100px;
            margin: 30px auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }

        .box {
            background: #161b22;
            border: 1px solid #30363d;
            border-radius: 12px;
            padding: 25px;
        }

        .box h2 {
            margin-bottom: 20px;
            color: #f0f6fc;
        }

        label {
            display: block;
            margin: 15px 0 7px;
            color: #8b949e;
        }

        input,
        textarea {
            width: 100%;
            padding: 12px;
            background: #0d1117;
            border: 1px solid #30363d;
            border-radius: 6px;
            color: white;
            outline: none;
        }

        input:focus,
        textarea:focus {
            border-color: #58a6ff;
        }

        textarea {
            resize: vertical;
            min-height: 100px;
        }

        button {
            width: 100%;
            margin-top: 20px;
            padding: 13px;
            border: none;
            border-radius: 7px;
            background: #238636;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
        }

        button:hover {
            background: #2ea043;
        }

        .secondary {
            background: #21262d;
        }

        .secondary:hover {
            background: #30363d;
        }

        #output {
            white-space: pre-wrap;
            background: #0d1117;
            border: 1px solid #30363d;
            border-radius: 8px;
            padding: 20px;
            min-height: 400px;
            overflow-x: auto;
            color: #c9d1d9;
        }

        .preview {
            margin-top: 20px;
            padding: 20px;
            background: white;
            color: #24292f;
            border-radius: 8px;
        }

        .preview h1 {
            margin-bottom: 10px;
        }

        .preview a {
            color: #0969da;
        }

        @media (max-width: 800px) {
            .container {
                grid-template-columns: 1fr;
            }

            header h1 {
                font-size: 25px;
            }
        }
    </style>
</head>

<body>

<header>
    <h1>🚀 GitHub Profile README Generator</h1>
    <p>Create your GitHub profile README easily</p>
</header>

<div class="container">

    <!-- INPUT SECTION -->
    <div class="box">

        <h2>📝 Profile Information</h2>

        <label>Your Name</label>
        <input type="text" id="name" placeholder="Methsara Sayuranga">

        <label>GitHub Username</label>
        <input type="text" id="github" placeholder="yourusername">

        <label>Short Bio</label>
        <textarea id="bio"
            placeholder="ICT Student | Programmer | Web Developer"></textarea>

        <label>Skills</label>
        <input type="text" id="skills"
            placeholder="HTML, CSS, JavaScript, C, Python">

        <label>About Me</label>
        <textarea id="about"
            placeholder="Write something about yourself..."></textarea>

        <button onclick="generateREADME()">
            🚀 Generate README
        </button>

        <button class="secondary" onclick="copyREADME()">
            📋 Copy README
        </button>

        <button class="secondary" onclick="downloadREADME()">
            ⬇ Download README.md
        </button>

    </div>


    <!-- OUTPUT SECTION -->
    <div class="box">

        <h2>💻 Generated README</h2>

        <div id="output">
            Your README will appear here...
        </div>

        <div class="preview" id="preview">
            <h1>Your Name</h1>
            <p>Your GitHub profile preview will appear here.</p>
        </div>

    </div>

</div>


<script>

function generateREADME() {

    const name =
        document.getElementById("name").value || "Your Name";

    const github =
        document.getElementById("github").value || "yourusername";

    const bio =
        document.getElementById("bio").value ||
        "ICT Student | Programmer | Web Developer";

    const skills =
        document.getElementById("skills").value ||
        "HTML, CSS, JavaScript";

    const about =
        document.getElementById("about").value ||
        "I love programming and learning new technologies.";

    const skillList = skills
        .split(",")
        .map(skill => `- ${skill.trim()}`)
        .join("\n");

    const readme = `# 👋 Hi, I'm ${name}

## 💻 About Me

${about}

### 🚀 What I Do

${bio}

### 🛠️ Skills

${skillList}

### 📊 GitHub

[![GitHub Profile](https://img.shields.io/badge/GitHub-${github}-181717?style=for-the-badge&logo=github)](https://github.com/${github})

### 🌐 Connect With Me

- 💻 GitHub: https://github.com/${github}

---

⭐ Thanks for visiting my profile!`;

    document.getElementById("output").textContent = readme;

    document.getElementById("preview").innerHTML = `
        <h1>👋 Hi, I'm ${name}</h1>

        <h2>💻 About Me</h2>
        <p>${about}</p>

        <h3>🚀 What I Do</h3>
        <p>${bio}</p>

        <h3>🛠️ Skills</h3>
        <ul>
            ${skills.split(",")
                .map(skill => `<li>${skill.trim()}</li>`)
                .join("")}
        </ul>

        <h3>📊 GitHub</h3>
        <p>
            <a href="https://github.com/${github}" target="_blank">
                github.com/${github}
            </a>
        </p>
    `;
}


function copyREADME() {

    const text =
        document.getElementById("output").textContent;

    navigator.clipboard.writeText(text);

    alert("README copied to clipboard! ✅");
}


function downloadREADME() {

    const text =
        document.getElementById("output").textContent;

    const blob =
        new Blob([text], { type: "text/markdown" });

    const url =
        URL.createObjectURL(blob);

    const link =
        document.createElement("a");

    link.href = url;
    link.download = "README.md";

    link.click();

    URL.revokeObjectURL(url);
}

</script>

</body>
</html>
