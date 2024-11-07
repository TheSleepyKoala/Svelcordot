<script lang="ts">
    import { onMount } from "svelte";
    import { DiscordHelper } from "$lib/utils/DiscordHelper";
    import { config } from "$lib/config";

    let godotCanvas: any;
    let godotInstance: any;
    let discordHelper: DiscordHelper;

    onMount(() => {
        if (
          window.location.hostname
            .includes("discordsays.com")
        ) {
          const originalFetch = window.fetch;
    
          window.fetch = (input, init) => {
            // Do not override well-formed absolute urls
            if (input.includes(".proxy/")) {
                return originalFetch(input, init).then((response) => {
                    // Godot insists on decompressing the body if it contains a Content-Encoding: gzip header.
                    // Apparently the Discord proxy decompresses them for us but leaves the header intact...
                    if (response.headers.get("Content-Encoding") == "gzip") {
                        // Response headers are immutable, so we need to create a new Response
                        var status = response.status;
                        var statusText = response.statusText;
                        var headers = new Headers();
                        for (const h of response.headers.entries()) {
                            if (h[0] != "Content-Encoding" && h[0] != "content-encoding") {
                                headers.append(h[0], h[1]);
                            }
                        }
                        return new Response(response.body, {status, statusText, headers});
                    }
                    
                    return response;
                });
            }
            
            // Use the saved original fetch function inside the redefined one
            return originalFetch(".proxy/" + input, init);
          };
        }

        discordHelper = new DiscordHelper();
        discordHelper.setupParentIframe();
        initializeGodot();
    });

    function initializeGodot() {
        const GODOT_CONFIG = {
            args: [],
            canvasResizePolicy: 2,
            executable: config.PRODUCT_NAME,
            experimentalVK: false,
            focusCanvas: true,
            gdextensionLibs: []
        };

        const script = document.createElement("script");
        script.src = config.PRODUCT_NAME + ".js";
        script.async = true;
        script.onload = () => {
            godotInstance = new Engine(GODOT_CONFIG);
            godotInstance.startGame();
        };
        document.body.appendChild(script);

        if (/iPhone|iPad|iPod|Android/i.test(navigator.userAgent)) {
            var meta = document.createElement("meta");
            meta.name = "viewport";
            meta.content = "width=device-width, height=device-height, initial-scale=1.0, user-scalable=no, shrink-to-fit=yes";
            document.getElementsByTagName("head")[0].appendChild(meta);
            
            godotCanvas = document.querySelector("#godot-canvas");
            godotCanvas.style.width = "100%";
            godotCanvas.style.height = "100%";
            godotCanvas.style.position = "fixed";
            document.body.style.textAlign = "left";
        }
    }
</script>
<body>
    <canvas 
        bind:this={godotCanvas}
        id="godot-canvas"
        tabindex="-1" 
        width="960"
        style="
            width: 100vw;
            height: 100vh;
            background: url('godotengine.png') center / cover; 
        "
    ></canvas>
</body>
<style>
    body {
        margin: 0px;
        background-color: #000000;
        padding: 0px;
        text-align: center;
        border: 0;
        height: 100vh;
        width: 100vw;
        overflow: hidden;
    }
</style>
