```html
<video id="screenVideo" autoplay playsinline controls></video><script>navigator.mediaDevices.getDisplayMedia({ video: true, audio: true }).then(stream => {const videoElement = document.getElementById("screenVideo");videoElement.srcObject = stream;stream.getVideoTracks()[0].onended = () => {videoElement.srcObject = null;};}).catch(error => {alert("Screen sharing failed: " + error.message);});</script>
```
