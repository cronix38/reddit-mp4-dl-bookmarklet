# reddit-mp4-dl-bookmarklet
Bookmarklet to download mp4 videos from reddit

Highlight the following code and drop it onto your bookmark bar to save it as a bookmarklet.
Then click on the bookmarklet while on a Reddit page containing a video to download the video

```js
javascript: (async () => {
    const baseUrl = document.getElementsByClassName('thumbnail')[0].getAttribute('href');
    const cases = [1080, 720, 480, 360, 240, 220];
    for (const c in cases) {
        const response = await fetch(`${baseUrl}/DASH_${cases[c]}.mp4`);
        if (response.status != 200) {continue;}
        const downloadLink = document.createElement('a');
        downloadLink.href = window.URL.createObjectURL(await response.blob());
        downloadLink.download = document.title + ".mp4";
        document.body.appendChild(downloadLink);
        downloadLink.click();
        document.body.removeChild(downloadLink);
        break;
    }
  })();
```
