https://chatgpt.com/?q=write a json script

let previousContent = null;
let sec = 2
const checkInterval = setInterval(function () {
    const element = document.getElementsByClassName("language-json")[0];
    if (element) {
        const currentContent = element.textContent.trim();
        if (currentContent && currentContent !== previousContent) { previousContent = currentContent }
        else if (currentContent === previousContent) {
            alert(element.textContent.trim());
            clearInterval(checkInterval);
        }
    }
}, sec * 1000);
