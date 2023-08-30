# ARTrack-Controller

Controlador de AR Tracking para Unity | Movimentação de um gameObject com AR Tracking como rastreador 

![Funcionando](https://github.com/flagar0/ARTrack-Controller/blob/main/gifs.gif?raw=true)
## Funcionalidades

- Definir um gameObject para se movimentar com o cubo
- Text para receber as informações e mostrar na tela
- Inverter direção x,y,z
- Ajustar sensibilidade
- Habilitar/Desabilitar Translação
- Habilitar/Desabilitar Rotação
- Definir os limites para o gameObject máximos/mínimos x,y,z


## Como usar para WEB
Adicionar o codigo `ARControllerWEB` no `EventSystem`, fazer a configurações e exportar.
Alterar codigo do `index.html` para mudar no final :

```diff
...
var script = document.createElement("script");
      script.src = loaderUrl;
      var Instancia = null;
      script.onload = () => {
        createUnityInstance(canvas, config, (progress) => {
          progressBarFull.style.width = 100 * progress + "%";
        }).then((unityInstance) => {
          loadingBar.style.display = "none";
+         Instancia = unityInstance;
          fullscreenButton.onclick = () => {
            unityInstance.SetFullscreen(1);
          };
        }).catch((message) => {
          alert(message);
        });
      };
      document.body.appendChild(script);
      
+var begin = true;
+	function sendWebsocketData(data) {
+		if(begin)
+			Instancia.SendMessage('EventSystem', 'MovimentaCuboWEB', data);
+	}			
+	var jsonWebSocket;
+	var ws = new WebSocket("ws://127.0.0.1:5678/"),messages = document.createElement 
+('ul');
+	ws.onmessage = function (event) {
+		date = new Date(Date.now())
+		sendWebsocketData(event.data.toString());
+	};      
```

