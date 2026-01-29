<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Abol Messenger</title>
    <style>
        body { font-family: sans-serif; background: #121212; color: white; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        #auth, #chat { background: #1e1e1e; padding: 20px; border-radius: 10px; box-shadow: 0 4px 15px rgba(0,0,0,0.5); width: 300px; }
        .hidden { display: none; }
        input { width: 100%; padding: 10px; margin: 10px 0; border: none; border-radius: 5px; box-sizing: border-box; }
        button { width: 100%; padding: 10px; background: #007bff; border: none; color: white; border-radius: 5px; cursor: pointer; }
        #messages { height: 200px; overflow-y: auto; border: 1px solid #333; padding: 10px; margin-bottom: 10px; display: flex; flex-direction: column; }
        .msg { margin-bottom: 8px; font-size: 14px; }
        .msg b { color: #007bff; }
    </style>
</head>
<body>

    <div id="auth">
        <h2>Вход в чат</h2>
        <input type="text" id="username" placeholder="Ваш юзернейм">
        <button onclick="login()">Войти</button>
    </div>

    <div id="chat" class="hidden">
        <h3 id="userDisplay"></h3>
        <div id="messages"></div>
        <input type="text" id="messageInput" placeholder="Сообщение...">
        <button onclick="sendMessage()">Отправить</button>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getFirestore, collection, addDoc, query, orderBy, onSnapshot, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

        // КОНФИГУРАЦИЯ FIREBASE (Вставь свои данные сюда!)
        const firebaseConfig = {
            apiKey: "ТВОЙ_КЛЮЧ",
            authDomain: "ТВОЙ_ДОМЕН",
            projectId: "ТВОЙ_ID",
            storageBucket: "ТВОЙ_БАКЕТ",
            messagingSenderId: "ID_ОТПРАВИТЕЛЯ",
            appId: "ID_ПРИЛОЖЕНИЯ"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        let currentUser = "";

        window.login = () => {
            const name = document.getElementById('username').value;
            if (name) {
                currentUser = name;
                document.getElementById('auth').classList.add('hidden');
                document.getElementById('chat').classList.remove('hidden');
                document.getElementById('userDisplay').innerText = "Я: " + currentUser;
                loadMessages();
            }
        };

        window.sendMessage = async () => {
            const text = document.getElementById('messageInput').value;
            if (text) {
                await addDoc(collection(db, "messages"), {
                    user: currentUser,
                    text: text,
                    createdAt: serverTimestamp()
                });
                document.getElementById('messageInput').value = "";
            }
        };

        function loadMessages() {
            const q = query(collection(db, "messages"), orderBy("createdAt", "asc"));
            onSnapshot(q, (snapshot) => {
                const msgDiv = document.getElementById('messages');
                msgDiv.innerHTML = "";
                snapshot.forEach((doc) => {
                    const data = doc.data();
                    msgDiv.innerHTML += `<div class="msg"><b>${data.user}:</b> ${data.text}</div>`;
                });
                msgDiv.scrollTop = msgDiv.scrollHeight;
            });
        }
    </script>
</body>
</html>
