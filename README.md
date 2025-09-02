<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Learn Smart</title>
  <link rel="icon" href="https://img.icons8.com/color/96/graduation-cap.png" />

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;800&display=swap" rel="stylesheet" />

  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #00c6ff, #0072ff);
      color: #222;
    }

    header {
      background: #fff;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      padding: 1rem 2rem;
      text-align: center;
      position: sticky;
      top: 0;
      z-index: 1000;
    }

    header h1 {
      font-size: 2.5rem;
      font-weight: 800;
      color: #0072ff;
      text-shadow: 2px 2px 5px rgba(0,0,0,0.3);
      margin: 0;
    }

    nav {
      margin-top: .5rem;
    }

    nav a {
      margin: 0 .8rem;
      text-decoration: none;
      font-weight: 600;
      color: #0072ff;
      transition: 0.3s;
    }

    nav a:hover {
      color: #00c6ff;
    }

    .container {
      padding: 2rem;
      max-width: 900px;
      margin: auto;
    }

    .section {
      background: #fff;
      border-radius: 12px;
      padding: 2rem;
      margin-bottom: 2rem;
      box-shadow: 0 6px 15px rgba(0,0,0,0.1);
    }

    h2 {
      color: #0072ff;
      margin-bottom: 1rem;
    }

    input, textarea, select, button {
      width: 100%;
      padding: .8rem;
      margin: .5rem 0 1rem;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 1rem;
    }

    button {
      background: linear-gradient(135deg, #00c6ff, #0072ff);
      color: #fff;
      font-weight: 600;
      cursor: pointer;
      border: none;
      transition: 0.3s;
    }

    button:hover {
      opacity: 0.9;
      transform: translateY(-2px);
    }

    .post {
      background: #f9f9f9;
      border-left: 5px solid #0072ff;
      padding: 1rem;
      margin-bottom: 1rem;
      border-radius: 8px;
    }

    .post h3 {
      margin: 0;
      color: #0072ff;
    }

    footer {
      background: #0072ff;
      color: #fff;
      text-align: center;
      padding: 1rem;
      margin-top: 2rem;
      border-top-left-radius: 12px;
      border-top-right-radius: 12px;
    }

    .whatsapp-btn {
      display: inline-block;
      background: #25d366;
      color: #fff !important;
      padding: .8rem 1.5rem;
      border-radius: 50px;
      font-weight: 600;
      text-decoration: none;
      transition: 0.3s;
    }

    .whatsapp-btn:hover {
      background: #1ebe5d;
    }
  </style>
</head>
<body>
  <header>
    <h1>Learn Smart</h1>
    <nav>
      <a href="#home">Home</a>
      <a href="#search">Search Topic</a>
      <a href="#submit">Submit Topic</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
      <a href="#terms">Terms</a>
    </nav>
  </header>

  <div class="container">
    <!-- Search Section -->
    <section id="search" class="section">
      <h2>Search Topics</h2>
      <input type="text" id="searchInput" placeholder="Type a keyword..." />
      <select id="sortSelect">
        <option value="newest">Sort by Newest</option>
        <option value="oldest">Sort by Oldest</option>
        <option value="az">Sort A → Z</option>
        <option value="za">Sort Z → A</option>
      </select>
      <div id="posts"></div>
    </section>

    <!-- Submit Section -->
    <section id="submit" class="section">
      <h2>Create Answer (Demo)</h2>
      <input type="text" id="titleInput" placeholder="Enter topic title" />
      <textarea id="contentInput" rows="5" placeholder="Write your answer..."></textarea>
      <button onclick="publishPost()">Publish Answer</button>
    </section>

    <!-- About Section -->
    <section id="about" class="section">
      <h2>About Learn Smart</h2>
      <p>Learn Smart is an academic support platform designed for university students across Nigeria. 
      Students can submit any topic they need help with, and answers will be provided clearly for their learning success.</p>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section">
      <h2>Contact</h2>
      <p>For submissions, use WhatsApp below:</p>
      <a class="whatsapp-btn" href="https://wa.me/2347083701096" target="_blank">Message on WhatsApp</a>
    </section>

    <!-- Terms Section -->
    <section id="terms" class="section">
      <h2>Terms</h2>
      <p>Learn Smart provides educational content to support students. 
      All materials are for academic guidance only. Users cannot edit or alter the platform’s content. 
      Respect is expected at all times.</p>
    </section>
  </div>

  <footer>
    <p>&copy; <span id="year"></span> Learn Smart | Powered in Nigeria</p>
  </footer>

  <script>
    const posts = [];
    const postsContainer = document.getElementById("posts");

    function publishPost() {
      const title = document.getElementById("titleInput").value;
      const content = document.getElementById("contentInput").value;
      if (!title || !content) {
        alert("Please fill in both fields.");
        return;
      }
      const post = {
        title,
        content,
        date: new Date()
      };
      posts.unshift(post);
      renderPosts();
      document.getElementById("titleInput").value = "";
      document.getElementById("contentInput").value = "";
    }

    function renderPosts() {
      postsContainer.innerHTML = "";
      let filtered = posts;
      const keyword = document.getElementById("searchInput").value.toLowerCase();
      if (keyword) {
        filtered = posts.filter(
          p =>
            p.title.toLowerCase().includes(keyword) ||
            p.content.toLowerCase().includes(keyword)
        );
      }

      const sort = document.getElementById("sortSelect").value;
      if (sort === "oldest") filtered = [...filtered].reverse();
      if (sort === "az") filtered.sort((a,b)=>a.title.localeCompare(b.title));
      if (sort === "za") filtered.sort((a,b)=>b.title.localeCompare(a.title));

      if (filtered.length === 0) {
        postsContainer.innerHTML = "<p>No topics found.</p>";
        return;
      }

      filtered.forEach(p => {
        const div = document.createElement("div");
        div.className = "post";
        div.innerHTML = `<h3>${p.title}</h3><p>${p.content}</p><small>${p.date.toLocaleString("en-NG")}</small>`;
        postsContainer.appendChild(div);
      });
    }

    document.getElementById("searchInput").addEventListener("input", renderPosts);
    document.getElementById("sortSelect").addEventListener("change", renderPosts);

    document.getElementById("year").textContent = new Date().getFullYear();
  </script>
</body>
</html>
