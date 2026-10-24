# No-links-texts-clean-image-zoom
# Clean Image Zoom

A bookmarklet for image search pages. It does two things:

1. **Cleans the grid.** Hides the captions, prices, store names and corner icons under each result, so you see only the images.
2. **Zooms in full resolution.** Clicking an image opens the original (not the blurry preview) centered on a dark background. Scroll to zoom, drag to pan.

## Install

**Easy way:** open the install page and drag the button to your bookmarks bar.

https://github.com/amandaman-hash/No-links-texts-clean-image-zoom/

(Show the bookmarks bar first with Ctrl+Shift+B on Windows/Linux or Cmd+Shift+B on Mac.)

**Manual way** (if dragging doesn't work):

1. Create a new bookmark in your browser (right-click the bookmarks bar, then Add page).
2. Name it `No Text Image Zoom`.
3. Paste the code below into the **URL** field. It must start with `javascript:` and have nothing before or after it.

```
javascript:(()=>{if(window.__lb5)return;window.__lb5=1;const o=document.createElement('div');o.style.cssText='position:fixed;inset:0;background:rgba(0,0,0,.88);display:none;align-items:center;justify-content:center;z-index:2147483647;cursor:zoom-out;overflow:hidden';const b=document.createElement('img');b.referrerPolicy='no-referrer';b.draggable=false;b.style.cssText='max-width:92vw;max-height:92vh;object-fit:contain;border-radius:8px;box-shadow:0 0 60px rgba(255,255,255,.25);cursor:grab;user-select:none';o.appendChild(b);document.body.appendChild(o);let s=1,tx=0,ty=0,tk=0,dr=0,mv=0,px=0,py=0,ht=0;const ap=()=>{b.style.transform='translate('+tx+'px,'+ty+'px) scale('+s+')'};const x=()=>{o.style.display='none'};o.addEventListener('click',e=>{if(e.target===o&&!mv)x()});document.addEventListener('keydown',e=>{if(e.key==='Escape')x()},true);o.addEventListener('wheel',e=>{e.preventDefault();const n=Math.min(10,Math.max(.5,s*(e.deltaY<0?1.15:1/1.15)));const cx=e.clientX-innerWidth/2,cy=e.clientY-innerHeight/2;tx=cx-(cx-tx)*(n/s);ty=cy-(cy-ty)*(n/s);s=n;ap()},{passive:false});b.addEventListener(%27mousedown%27,e=>{e.preventDefault();dr=1;mv=0;px=e.clientX;py=e.clientY});window.addEventListener(%27mousemove%27,e=>{if(!dr)return;const dx=e.clientX-px,dy=e.clientY-py;if(Math.abs(dx)+Math.abs(dy)>2)mv=1;tx+=dx;ty+=dy;px=e.clientX;py=e.clientY;ap()});window.addEventListener(%27mouseup%27,()=>{dr=0;setTimeout(()=>{mv=0},0)});const c=()=>{document.querySelectorAll(%27img%27).forEach(i=>{if(i.dataset.cl||o.contains(i)||i.offsetWidth<150)return;let n=i;while(n.parentElement&&n.parentElement!==document.body){if(n!==i&&n.innerText&&n.innerText.trim())break;n=n.parentElement}let u=i;while(u!==n){const p=u.parentElement;[...p.children].forEach(q=>{if(q!==u)q.style.display=%27none%27});u=p}i.dataset.cl=1})};const f=t=>{let n=t;for(let k=0;k<10&&n&&n!==document.body;k++){const m=n.querySelectorAll?n.querySelectorAll(%27img[data-cl]%27):[];if(m.length===1)return m[0];if(m.length>1)return null;n=n.parentElement}return null};const g=i=>{let n=i;for(let k=0;k<8&&n&&n!==document.body;k++){const a=n.tagName===%27A%27&&n.href.includes(%27imgurl=%27)?n:n.querySelector&&n.querySelector(%27a[href*="imgurl="]%27);if(a){try{return new URL(a.href,location.href).searchParams.get(%27imgurl%27)}catch(e){}}n=n.parentElement}return null};const pc=new Map();const pre=i=>{const u=g(i);if(!u)return null;if(!pc.has(u)){const t=new Image();t.referrerPolicy=%27no-referrer%27;t.src=u;pc.set(u,t)}return u};window.addEventListener(%27mouseover%27,e=>{clearTimeout(ht);const i=f(e.target);if(!i)return;ht=setTimeout(()=>pre(i),120)},true);window.addEventListener(%27mousedown%27,e=>{const i=f(e.target);if(i)setTimeout(()=>pre(i),0)},true);window.addEventListener(%27click%27,e=>{const i=f(e.target);if(!i)return;e.preventDefault();e.stopImmediatePropagation();const my=++tk;s=1;tx=ty=0;ap();b.src=i.currentSrc||i.src;o.style.display=%27flex%27;const u=pre(i);if(u){const t=pc.get(u);if(t.complete&&t.naturalWidth){b.src=u}else{t.addEventListener(%27load%27,()=>{if(my===tk)b.src=u})}}},true);c();new MutationObserver(c).observe(document.body,{childList:true,subtree:true})})();
```

## Usage

1. Run an image search.
2. Click the bookmark **once** per page load. Reload or a new search means click it again.
3. Click any image to open it.

| Action | Control |
| --- | --- |
| Open image | Click it |
| Zoom in / out | Scroll up / down (0.5x to 10x, centered on the cursor) |
| Pan | Click and drag |
| Close | Click the dark background, or press Esc |

## How it works

- The cleaner walks up from each large image and hides every sibling element that is not part of the image itself.
- Search results link to the original image address. The script reads that address and loads the full-size file instead of the thumbnail.
- Pausing the cursor on an image (about 120 ms) or pressing the mouse button starts downloading the original early, so it is often ready by the time you click.
- Everything runs locally in your browser. The script makes no requests of its own except loading the images you view, and it collects no data.

## Known limitations

- **Fragile by nature.** It depends on the page structure of the search site, so it can break whenever that structure changes. This is best-effort software.
- **Data use.** Pausing on tiles downloads their full-size originals, which uses more data than normal browsing. On a metered connection, use it sparingly.
- **Some results stay low quality.** Tiles that don't expose the original image address (shopping results, for example) show only the thumbnail.
- **Blocked images.** Some sites refuse to serve their images to other pages. Those stay at thumbnail quality.
- **Desktop only.** It is designed for a mouse and scroll wheel, and bookmarklets are limited on mobile browsers.
- **Once per page load.** The bookmark has to be clicked again after each reload or new search.

## Troubleshooting

- **Nothing happens when I click the bookmark.** Check that the URL field starts exactly with `javascript:` and has no stray characters before or after. Chrome also removes `javascript:` if you type it into the address bar, so use a bookmark.
- **Captions are back after clicking an image.** Reload the page and click the bookmark again.
- **Images stay blurry.** The result probably doesn't expose its original (see limitations).

## Reporting a bug

Open an issue and include:

- Your browser and version
- The search page address (remove any personal info)
- What you expected and what happened
- Any red errors shown in the browser console (press F12, then the Console tab)

## Browser extension

The same logic is also available as a Chrome/Edge extension, which runs automatically without clicking a bookmark. See the `extension/` folder and the Releases page. To install:

1. Download and unzip the latest release.
2. Open `chrome://extensions` and turn on **Developer mode**.
3. Click **Load unpacked** and choose the unzipped folder.

## Contributing

Pull requests are welcome, especially fixes for when the page structure changes. Please test in a clean browser profile before submitting.

## Disclaimer

This project is not affiliated with, endorsed by, or sponsored by any search engine company. Product and company names are trademarks of their respective owners. You are responsible for respecting the terms of the sites you use it on and the copyright of images you view.

