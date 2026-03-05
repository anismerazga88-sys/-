<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>موقع القصص الأسطوري</title>

<!-- خطوط Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&family=Lato:wght@400;700&family=Roboto:wght@400;700&display=swap" rel="stylesheet">

<style>
  :root {
    --bg-color: #f4f1ed;
    --text-color: #333;
    --card-bg: white;
    --card-shadow: rgba(0,0,0,0.1);
  }
  [data-theme="dark"] {
    --bg-color: #1c1c1c;
    --text-color: #eee;
    --card-bg: #2c2c2c;
    --card-shadow: rgba(255,255,255,0.1);
  }

  body {
    font-family: 'Cairo', sans-serif;
    margin: 0;
    background: var(--bg-color);
    color: var(--text-color);
    transition: background 0.3s, color 0.3s;
  }

  header {
    background: #6c5b7b;
    color: white;
    padding: 15px 20px;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    align-items: center;
    box-shadow: 0 3px 6px rgba(0,0,0,0.15);
  }
  header .logo { font-size: 1.5em; font-weight: bold; }
  header nav { display: flex; flex-wrap: wrap; gap:10px; }
  header nav a, .theme-btn {
    color: white;
    text-decoration: none;
    padding: 6px 12px;
    border-radius: 5px;
    background: #355c7d;
    cursor: pointer;
    transition: 0.3s;
  }
  header nav a:hover, .theme-btn:hover { background: #6c5b7b; }

  main { padding: 15px; max-width: 750px; margin: auto; }

  h1 { text-align: center; margin-bottom: 15px; color: var(--text-color); }

  /* نموذج كتابة القصة */
  .story-form {
    background: var(--card-bg);
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 3px 10px var(--card-shadow);
    margin-bottom: 20px;
    transition: transform 0.2s;
  }
  .story-form:hover { transform: translateY(-2px); }
  .story-form input[type="text"], .story-form textarea, .story-form select {
    width: 100%;
    padding: 12px;
    margin-bottom: 12px;
    border-radius: 8px;
    border: 1px solid #ccc;
    font-size: 1em;
  }
  .story-form button { background: #355c7d; color: white; border: none; padding: 12px; border-radius: 8px; cursor: pointer; font-size: 1em; width: 100%; }
  .story-form button:hover { background: #6c5b7b; }

  /* معاينة القصة */
  #preview {
    background: #fef7ef;
    padding: 15px;
    border-radius: 8px;
    margin-bottom: 20px;
    display: none;
    border: 1px solid #ffd3b6;
  }

  /* قائمة القصص */
  .story-list { list-style: none; padding: 0; display: grid; gap:15px; grid-template-columns: 1fr; }
  .story-list li {
    background: var(--card-bg);
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 3px 10px var(--card-shadow);
    position: relative;
    transition: transform 0.2s;
  }
  .story-list li:hover { transform: translateY(-2px); }
  .story-list li h2 { margin: 0 0 10px 0; color: var(--text-color); }
  .story-list li p { margin: 0 0 10px 0; white-space: pre-wrap; color: var(--text-color); }

  .story-actions {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    margin-bottom: 10px;
  }
  .story-actions button {
    flex: 1;
    padding: 8px;
    border-radius: 6px;
    border: none;
    cursor: pointer;
    font-weight: bold;
  }
  .edit-btn { background: #f39c12; color: white; }
  .delete-btn { background: #e74c3c; color: white; }
  .edit-btn:hover { background: #e67e22; }
  .delete-btn:hover { background: #c0392b; }

  /* تعديل عصري */
  .edit-area {
    display: none;
    margin-top: 10px;
    background: var(--bg-color);
    padding:10px;
    border-radius:10px;
  }
  .edit-area input, .edit-area textarea, .edit-area select {
    width: 100%;
    padding: 10px;
    margin-bottom: 8px;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 0.95em;
  }
  .edit-area button { padding: 10px; border-radius: 6px; font-weight: bold; margin-bottom:5px; }

  footer {
    text-align: center;
    padding: 15px;
    margin-top: 20px;
    color: #666;
    font-size: 0.9em;
  }

  @media (max-width: 700px) {
    header { flex-direction: column; align-items: flex-start; }
    header nav { flex-direction: column; width: 100%; }
    header nav a, .theme-btn { margin: 5px 0; width: 100%; text-align: center; }
  }
</style>
</head>
<body>

<header>
  <div class="logo">موقع القصص الأسطوري</div>
  <nav>
    <a href="#write">كتابة قصة</a>
    <a href="#stories">القصص المنشورة</a>
    <button class="theme-btn" onclick="toggleTheme()">تغيير الوضع</button>
    <select id="fontSelect" onchange="changeFont()">
      <option value="Cairo">Cairo</option>
      <option value="Roboto">Roboto</option>
      <option value="Lato">Lato</option>
    </select>
  </nav>
</header>

<main>
  <section id="write">
    <h1>كتابة قصة جديدة</h1>
    <form class="story-form" id="storyForm">
      <input type="text" id="storyTitle" placeholder="عنوان القصة" required>
      <textarea id="storyContent" rows="6" placeholder="اكتب نص القصة هنا..." required></textarea>
      <button type="submit">نشر القصة</button>
    </form>
    <div id="preview">
      <h3>معاينة القصة</h3>
      <h4 id="previewTitle"></h4>
      <p id="previewContent"></p>
    </div>
  </section>

  <section id="stories">
    <h1>القصص المنشورة</h1>
    <ul class="story-list" id="storyList"></ul>
  </section>
</main>

<footer>
  حقوق النشر © 2026 | تصميم أسطوري للقصص
</footer>

<script>
let stories = JSON.parse(localStorage.getItem('stories') || '[]');
const storyList = document.getElementById('storyList');
const form = document.getElementById('storyForm');
const preview = document.getElementById('preview');
const previewTitle = document.getElementById('previewTitle');
const previewContent = document.getElementById('previewContent');
const fontSelect = document.getElementById('fontSelect');

function renderStories(){
  storyList.innerHTML = '';
  stories.forEach((story,index)=>{
    const li = document.createElement('li');
    li.innerHTML=`
      <h2>${story.title}</h2>
      <p>${story.content}</p>
      <div class="story-actions">
        <button class="edit-btn" onclick="toggleEdit(${index})">تعديل</button>
        <button class="delete-btn" onclick="deleteStory(${index})">حذف</button>
      </div>
      <div class="edit-area" id="edit-${index}">
        <input type="text" id="editTitle-${index}" value="${story.title}">
        <textarea id="editContent-${index}" rows="4">${story.content}</textarea>
        <button onclick="saveEdit(${index})" style="background:#355c7d;color:white;">حفظ</button>
        <button onclick="toggleEdit(${index})" style="background:#ccc;">إلغاء</button>
      </div>
    `;
    storyList.appendChild(li);
  });
}

renderStories();

// معاينة
form.addEventListener('input', ()=>{
  const title = document.getElementById('storyTitle').value.trim();
  const content = document.getElementById('storyContent').value.trim();
  if(title||content){
    preview.style.display='block';
    previewTitle.textContent=title||'عنوان القصة';
    previewContent.textContent=content||'محتوى القصة يظهر هنا...';
  }else{
    preview.style.display='none';
  }
});

form.addEventListener('submit',(e)=>{
  e.preventDefault();
  const title=document.getElementById('storyTitle').value.trim();
  const content=document.getElementById('storyContent').value.trim();
  if(title && content){
    stories.unshift({title,content});
    localStorage.setItem('stories',JSON.stringify(stories));
    renderStories();
    form.reset();
    preview.style.display='none';
    alert('تم نشر القصة بنجاح!');
  }
});

function deleteStory(index){
  if(confirm('هل أنت متأكد من حذف هذه القصة؟')){
    stories.splice(index,1);
    localStorage.setItem('stories',JSON.stringify(stories));
    renderStories();
  }
}

function toggleEdit(index){
  const editArea=document.getElementById(`edit-${index}`);
  editArea.style.display = editArea.style.display==='block'?'none':'block';
}

function saveEdit(index){
  const newTitle=document.getElementById(`editTitle-${index}`).value.trim();
  const newContent=document.getElementById(`editContent-${index}`).value.trim();
  if(newTitle && newContent){
    stories[index]={title:newTitle,content:newContent};
    localStorage.setItem('stories',JSON.stringify(stories));
    renderStories();
  }else{
    alert('يجب ملء العنوان والمحتوى');
  }
}

// Light/Dark Mode
function toggleTheme(){
  document.body.dataset.theme = document.body.dataset.theme==='dark'?'light':'dark';
}

// تغيير الخط
function changeFont(){
  document.body.style.fontFamily = fontSelect.value;
}
</script>
</body>
</html>
