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
2. Name it `Image Zoom`.
3. Paste the code below into the **URL** field. It must start with `javascript:` and have nothing before or after it.

```
PASTE THE CONTENTS OF bookmarklet.min.js HERE
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

## License

MIT. See [LICENSE](LICENSE).
