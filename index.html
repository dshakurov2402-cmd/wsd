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
        input { width: 100%; padding: 10px; margin: 10px 0; border: none; border-radius: 5px; box-sizing: border-box; background: #333; color: white; }
        button { width: 100%; padding: 10px; background: #007bff; border: none; color: white; border-radius: 5px; cursor: pointer; }
        #messages { height: 250px; overflow-y: auto; border: 1px solid #333; padding: 10px; margin-bottom: 10px; display: flex; flex-direction: column; background: #181818; }
        .msg { margin-bottom: 8px; font-size: 14px; padding: 5px; border-radius: 4px; background: #252525; }
        .msg b { color: #007bff; }
    </style>
</head>
<body>

    <div id="auth">
        <h2>Abol Chat</h2>
        <input type="text" id="username" placeholder="Твой юзернейм">
        <button onclick="login()">Войти</button>
    </div>

    <div id="chat" class="hidden">
        <h3 id="userDisplay"></h3>
        <div id="messages"></div>
        <input type="text" id="messageInput" placeholder="Написать другу...">
        <button onclick="sendMessage()">Отправить</button>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getFirestore, collection, addDoc, query, orderBy, onSnapshot, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

        // ТВОИ КЛЮЧИ ИЗ FIREBASE
        const firebaseConfig = {
            apiKey: "AIzaSyBz8fnaJ_mpCE5Vv83doxBb6nTybDSBmlI",
            authDomain: "kaka-chat-39bb6.firebaseapp.com",
            projectId: "kaka-chat-39bb6",
            storageBucket: "kaka-chat-39bb6.firebasestorage.app",
            messagingSenderId: "927391255601",
            appId: "1:927391255601:web:1f83128108dc1ca2831910",
            measurementId: "G-D9CJ12HC8K"
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
                document.getElementById('userDisplay').innerText = "Вы вошли как: " + currentUser;
                loadMessages();
            }
        };

        window.sendMessage = async () => {
            const textInput = document.getElementById('messageInput');
            const text = textInput.value;
            if (text) {
                await addDoc(collection(db, "messages"), {
                    user: currentUser,
                    text: text,
                    createdAt: serverTimestamp()
                });
                textInput.value = "";
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
