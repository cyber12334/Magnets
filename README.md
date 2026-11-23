# Self-hosted AR refrigerator magnet

This is a small, static WebAR project using A-Frame and MindAR Image Tracking.
It has no paid services, account requirement, trial, or application server.
The A-Frame and MindAR JavaScript libraries load from free public CDNs; the
target image, video, and page are hosted as ordinary static files.

## Project files

```text
ar-magnet/
├── index.html
├── targets.mind   # placeholder; replace with the compiled target file
├── video.mp4      # placeholder; replace with your video
└── README.md
```

The two placeholder files are instructional text, not usable media. Replace
them with the real compiled target and MP4 before testing or publishing.

## 1. Design the magnet in Canva

1. Create the magnet artwork in Canva at the final print dimensions. Keep it
   distinctive and high contrast: use clear shapes, varied colors, and
   details that do not repeat across the image.
2. **Before adding the QR code**, export the magnet artwork as a high-quality
   PNG or JPG. This clean artwork will be used to create the image-tracking
   target.
3. Keep the final artwork available; you will add the QR code to it after the
   target is compiled.

## 2. Compile `targets.mind`

1. Open the free MindAR Image Target Compiler:
   <https://hiukim.github.io/mind-ar-js-doc/tools/compile/>
2. Upload the Canva magnet graphic exported **without** the QR code.
3. Compile the image target, then download the generated `.mind` file.
4. Put it in this folder and name it exactly `targets.mind`, replacing the
   placeholder. The first compiled image corresponds to `targetIndex: 0` in
   `index.html`.
5. Add a **static QR code** to the Canva artwork that points to the final
   hosted URL for this project. A QR code made in Canva avoids a separate
   dynamic QR service. Export the updated design as the final print file.

The QR code is intentionally not part of the tracking target: it can reduce
image matching reliability and is not needed to recognize the magnet.

## 3. Prepare the video

1. Make a short MP4 video for the AR animation. For broad mobile compatibility,
   use H.264 video with AAC audio (or no audio). Keep the file reasonably
   small so it loads quickly over mobile connections.
2. Match the video's aspect ratio to the magnet graphic and the `<a-video>`
   plane in `index.html`. The video plane defaults to portrait 3:4
   (`width="0.75" height="1"`). For a square magnet use `1` by `1`; for a
   landscape 4:3 magnet use `1.33` by `1`. Adjust both dimensions in the HTML
   comments and `<a-video>` element if your design has another ratio. The
   video itself should have the same ratio to avoid stretching or empty bars.
3. A free video encoder such as HandBrake can reduce resolution/bitrate if
   needed. Export without black bars and use a resolution suitable for a
   phone-sized overlay.
4. Copy the MP4 into this folder as `video.mp4`, replacing the placeholder.

## 4. Test locally

Web camera access requires a secure context: use `localhost` for local tests
or HTTPS after deployment. Opening `index.html` directly as a `file://` URL
usually will not work.

1. Open the `ar-magnet` folder in VS Code.
2. Install/use the free **Live Server** VS Code extension, then choose **Go
   Live** on `index.html`. Alternatively, serve the folder with any local
   static HTTP server on `localhost`.
3. Open the local URL on a phone on the same network if your server supports
   it over HTTPS; otherwise test on the computer's browser with a webcam.
   Grant camera access and point the camera at the printed magnet or the
   exact artwork used to compile the target.
4. The page starts muted. When the target is found, the video plays and the
   **Tap for Sound** button appears. Tap it to enable audio. Check the browser
   console if camera access, asset loading, or target detection fails.

## 5. Deploy for free

### Netlify Drop

1. Ensure `index.html`, the real `targets.mind`, and the real `video.mp4` are
   all in `ar-magnet/`.
2. Open <https://app.netlify.com/drop> and drop the **contents** of this
   folder (or the folder itself if the page accepts it).
3. Wait for the deploy and open the HTTPS site URL. Use that URL as the Canva
   QR code destination. If you change the destination later, update and
   re-export the printed QR code.

### GitHub Pages

1. Create a GitHub repository and upload the contents of `ar-magnet/` to its
   root, including the two real media files.
2. In the repository, open **Settings → Pages**, select deployment from the
   `main` branch and `/ (root)`, then save.
3. Wait for the Pages build and open the provided HTTPS URL. If the files are
   in a repository subfolder instead, the published page URL includes that
   folder path.
4. Use the final HTTPS page URL in Canva's static QR code and export the
   print-ready magnet.

## Print and troubleshooting tips

- Matte paper or a matte laminate reduces reflections under indoor lighting
  compared with a high-gloss finish. Glare can make image tracking less
  reliable.
- Print the same artwork that was compiled as the target; avoid changing its
  crop, scale, or major colors.
- If detection is unreliable, use a sharper, more visually varied graphic,
  reduce glare, and make sure the target has enough visible detail. Recompile
  after changing the graphic.
- Confirm that both media placeholders were replaced and that filenames and
  letter case exactly match `targets.mind` and `video.mp4`.
