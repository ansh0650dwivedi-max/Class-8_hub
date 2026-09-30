# Class-8_hub
Class 8 UP Board Study Portal
<!DOCTYPE html>
<html lang="hi">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <title>Class 8 UP Board - Media & Video Hub</title>
 <style>
 :root {
 --bg-color: #0f172a;
 --card-bg: #1e293b;
 --text-color: #f8fafc;
 --accent-color: #38bdf8;
 --btn-bg: #0284c7;
 --btn-hover: #0369a1;
 }
 * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, 
Verdana, sans-serif; }
 body { background-color: var(--bg-color); color: var(--text-color); padding: 20px; 
transition: all 0.3s ease; }
 .container { max-width: 900px; margin: 0 auto; }
 header { text-align: center; margin-bottom: 25px; }
 header h1 { color: var(--accent-color); font-size: 2.2rem; margin-bottom: 8px; }
 .create-box { background-color: var(--card-bg); padding: 20px; border-radius: 12px; margin-
bottom: 30px; box-shadow: 0 4px 10px rgba(0, 0, 0, 0.4); }
 .form-group { margin-bottom: 15px; }
 .form-group label { display: block; margin-bottom: 5px; font-weight: 600; color: #94a3b8; }
 .form-group input, .form-group textarea, .form-group select { width: 100%; padding: 10px 14px; border-radius: 8px; border: 1px solid #334155; background-color: #0f172a; color: #fff; 
font-size: 0.95rem; outline: none; }
 .form-group input:focus, .form-group textarea:focus { border-color: var(--accent-color); }
 .file-inputs { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
 .btn-add { width: 100%; padding: 12px; border-radius: 8px; border: none; background-color: 
var(--btn-bg); color: white; font-weight: bold; font-size: 1rem; cursor: pointer; transition: 
background-color 0.2s; }
 .btn-add:hover { background-color: var(--btn-hover); }
 .feed { display: flex; flex-direction: column; gap: 25px; }
 .post-card { background-color: var(--card-bg); border-radius: 12px; padding: 20px; box-
shadow: 0 4px 6px rgba(0, 0, 0, 0.3); position: relative; }
 .post-title { font-size: 1.4rem; color: var(--accent-color); margin-bottom: 8px; }
 .post-desc { color: #cbd5e1; font-size: 0.95rem; margin-bottom: 15px; white-space: pre-
line; }
 .video-container { position: relative; padding-bottom: 56.25%; height: 0; border-radius: 
8px; overflow: hidden; margin-bottom: 15px; background: #000; }
 .video-container iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; 
border: none; }
 .attachments { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 15px; padding-top: 
15px; border-top: 1px solid #334155; }
 .attached-photo { max-width: 100%; max-height: 300px; border-radius: 8px; object-fit: 
cover; }
 .file-badge { display: inline-flex; align-items: center; gap: 8px; background-color: 
#0f172a; padding: 8px 12px; border-radius: 6px; color: var(--accent-color); text-decoration: 
none; font-size: 0.88rem; border: 1px solid #334155; }
 .file-badge:hover { background-color: #1e293b; }
 .delete-btn { position: absolute; top: 15px; right: 15px; background-color: #ef4444; color: 
white; border: none; padding: 6px 12px; border-radius: 6px; cursor: pointer; font-size: 0.8rem; 
font-weight: bold; }
 .delete-btn:hover { background-color: #dc2626; }
 @media (max-width: 600px) { .file-inputs { grid-template-columns: 1fr; } }
 </style>
</head>
<body>
 <div class="container">
 <header>
 <h1>Class 8 UP Board Study Hub</h1>
 <p>YouTube वीɟडियो, नोट्स और फ़ाइलें एक साथ शेयर करें</p>
 </header>
 <div class="create-box">
 <div class="form-group">
 <label for="postTitle">पाठ / ɟवषय का नाम (Title):</label>
 <input type="text" id="postTitle" placeholder="जैसे: गɢणित - अध्याय 1 पɝरमेय संख्याएँ">
 </div>
 <div class="form-group">
 <label for="postDesc">ɟववरणि / मुख्य बातें (Description):</label>
 <textarea id="postDesc" rows="3" placeholder="यहाँ नोट्स या मुख्य सवाल ɡलखें..."></textarea>
 </div>
 <div class="form-group">
 <label for="youtubeUrl">YouTube क्लास वीɟडियो ɭलंक:</label>
 <input type="text" id="youtubeUrl" placeholder="https://www.youtube.com/watch?v=...">
 </div>
 <div class="file-inputs">
 <div class="form-group">
 <label for="photoInput">इमेज / डिायग्राम (Image):</label>
 <input type="file" id="photoInput" accept="image/*">
 </div>
 <div class="form-group">
 <label for="fileInput">PDF नोट्स अटैच करें:</label>
 <input type="file" id="fileInput" accept=".pdf,.doc,.docx,.txt">
 </div>
 </div>
 <button class="btn-add" onclick="createPost()">स्टडिी पोस्ट पɜÍलश करें</button>
 </div>
 <div class="feed" id="postsFeed"></div>
 </div>
 <script>
 function getYouTubeID(url) {
 const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^# mp;\?]*).*/;
 const match = url.match(regExp);
 return (match && match[2].length === 11) ? match[2] : null;
 }
 function readFileAsDataURL(file) {
 return new Promise((resolve, reject) => {
 if (!file) return resolve(null);
 const reader = new FileReader();
 reader.onload = () => resolve({ name: file.name, data: reader.result });
 reader.onerror = reject; reader.readAsDataURL(file);
 });
 }
 async function createPost() {
 const title = document.getElementById('postTitle').value.trim();
 const desc = document.getElementById('postDesc').value.trim();
 const ytUrl = document.getElementById('youtubeUrl').value.trim();
 const photoFile = document.getElementById('photoInput').files[0];
 const docFile = document.getElementById('fileInput').files[0];
 const ytID = ytUrl ? getYouTubeID(ytUrl) : null;
 if (!title && !ytID && !photoFile && !docFile) {
 alert('कृ पया कम से कम एक वीɟडियो, टाइटल या फ़ाइल जोड़ें!');
 return;
 }
 const photoData = await readFileAsDataURL(photoFile);
 const docData = await readFileAsDataURL(docFile);
 const postObj = {
 id: Date.now(),
 title: title || 'Class 8 Notes',
 desc: desc,
 youtubeID: ytID,
 photo: photoData,
 document: docData
 };
 savePostToStorage(postObj);
 renderPost(postObj);
 document.getElementById('postTitle').value = '';
 document.getElementById('postDesc').value = '';
 document.getElementById('youtubeUrl').value = '';
 document.getElementById('photoInput').value = '';
 document.getElementById('fileInput').value = '';
 }
 function renderPost(post) {
 const feed = document.getElementById('postsFeed');
 const card = document.createElement('div');
 card.className = 'post-card';
 card.id = `post-${post.id}`;
 let contentHTML = `<button class="delete-btn" onclick="deletePost(${post.id})">ɟडिलीट</
button>`;
 if (post.title) contentHTML += `<h2 class="post-title">${escapeHTML(post.title)}</h2>`;
 if (post.desc) contentHTML += `<p class="post-desc">${escapeHTML(post.desc)}</p>`;
 if (post.youtubeID) {
 contentHTML += `<div class="video-container"><iframe src="https://www.youtube.com/embed/
${post.youtubeID}" allowfullscreen></iframe></div>`;
 }
 if (post.photo || post.document) {
 contentHTML += `<div class="attachments">`;
 if (post.photo) contentHTML += `<img src="${post.photo.data}" class="attached-photo">`;
 if (post.document) {
 contentHTML += `<a href="${post.document.data}" download="${post.document.name}" 
class="file-badge"> ${escapeHTML(post.document.name)} (डिाउनलोडि)</a>`;
 }
 contentHTML += `</div>`;
 }
 card.innerHTML = contentHTML;
 feed.prepend(card);
 }
 function escapeHTML(str) {
 return str.replace(/[&<>'""]/g, tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": 
'&#39;', '"': '&quot;' }[tag] || tag));
 }
 function savePostToStorage(post) {
 const posts = JSON.parse(localStorage.getItem('class8Posts') || '[]');
 posts.push(post);
 localStorage.setItem('class8Posts', JSON.stringify(posts));
 }
 function loadPosts() {
 const posts = JSON.parse(localStorage.getItem('class8Posts') || '[]');
 posts.forEach(post => renderPost(post));
 }
 function deletePost(id) {
 if (!confirm('क्या आप इसे ɟडिलीट करना चाहते हैं?')) return;
 let posts = JSON.parse(localStorage.getItem('class8Posts') || '[]');
 posts = posts.filter(p => p.id !== id);
 localStorage.setItem('class8Posts', JSON.stringify(posts));
 const card = document.getElementById(`post-${id}`);
 if (card) card.remove();
 } window.onload = loadPosts;
