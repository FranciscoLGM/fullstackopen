sequenceDiagram
participant User
participant Browser
participant Server

    User->>Browser: Escribe una nueva nota en el campo de texto y hace clic en "Save"
    Browser->>Server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate Server
    Note right of Server: El servidor recibe la nueva nota y la almacena en el archivo data.json
    Server-->>Browser: Respuesta de redirección (302) a /exampleapp/notes
    deactivate Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate Server
    Server-->>Browser: HTML document
    deactivate Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate Server
    Server-->>Browser: the css file
    deactivate Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate Server
    Server-->>Browser: the JavaScript file
    deactivate Server

    Note right of Browser: El navegador ejecuta el código JavaScript que obtiene el JSON del servidor

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate Server
    Server-->>Browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate Server

    Note right of Browser: El navegador ejecuta la función de callback que renderiza las notas, incluyendo la nueva nota añadida
