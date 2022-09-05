# Overviews

- The Web offers a wide variety of APIs to perform various useful tasks.
- Links
    + https://developer.mozilla.org/en-US/docs/Web/Reference/API
- Popular APIs
    + DOM (Document Object Model)
        * Why?
            - https://www.quora.com/Why-do-we-need-a-DOM-Why-cant-we-just-manipulate-the-HTML-I-would-like-to-know-the-reasoning-behind-it-and-why-the-concept-of-a-DOM-was-born
            - https://en.wikipedia.org/wiki/Document_Object_Model#History
        * Representing a document using a logical tree: each node
          contains objects
        * With DOM, you can change the document's structure, style, and
          content
        * Nodes also have event handlers attached to them. Once an event
          is triggered, the event handlers get executed.
        * EventTarget interface: is implemented by objects that can
          receive events and may have listeners for them.
            - `obj.addEventListener('eventName', callback)`
        * Window interface represents a window containing a DOM document
            - the global `window` variable represents the window in
              which the script is running
        * Node interface represents a node in the DOM tree
            - Node extends EventTarget
            - `node.nodeValue`: get/set node's value as string
            - `node.nodeType`: 1: element node, 2: attribute node, 3:
              text node, 8: comment node
            - `node.textContent`: get/set node's text content (text
              node)
        * Document interface represents the entry point for the DOM tree
            - Document extends Node extends EventTarget
        * Element interface represents an element in a document
            - `element.innerHTML`: parses text as HTML content
        * HTMLElement interface represents a HTML element
            - `htmlElement.innerText`: text and applies styles
    + XMLHttpRequest: using in AJAX technique
    + WebSocket: full-duplex communication between server and client
        * Client only: WebSocket interface: https://developer.mozilla.org/en-US/docs/Web/API/WebSocket
        * Server and Client:
            * Plain implementations:
                - ws (NodeJS built-in): https://github.com/websockets/ws
                - uWebSockets: https://github.com/uNetworking/uWebSockets.js
                    + https://github.com/uNetworking/uWebSockets (C++)
            * More abstraction
                - socket.io: https://github.com/socketio/socket.io
                    + using engine.io underneath: https://github.com/socketio/engine.io
                - deepstream.io: https://github.com/deepstreamIO/deepstream.io
                - primus: https://github.com/primus/primus
                    + another abstract layer for real-time frameworks
                    + you can swap in and out different real-time frameworks

# fetch API

- Alternative: axios, etc.
- https://blog.logrocket.com/axios-vs-fetch-best-http-requests/
