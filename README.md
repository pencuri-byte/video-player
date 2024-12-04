Untuk membuat shortcut menuju bagian bahasa Inggris dan bahasa Indonesia dalam README, Anda bisa menggunakan tautan internal (anchor links). Berikut adalah contoh bagaimana Anda bisa melakukannya:

### README.md

```markdown
# Video Player dengan Playlist dan Mode Gelap

[English Version](#english-version) | [Versi Bahasa Indonesia](#versi-bahasa-indonesia)

## Versi Bahasa Indonesia

Proyek ini adalah contoh implementasi pemutar video dengan fitur playlist dan mode gelap menggunakan HTML, CSS, dan JavaScript.

### Fitur

- Memutar video dari folder yang dipilih.
- Navigasi video dengan tombol "Previous" dan "Next".
- Playlist video yang dapat diklik untuk memutar video tertentu.
- Mode gelap yang dapat diaktifkan dengan switch.

### Cara Menggunakan

1. Pilih folder yang berisi video dengan mengklik input file.
2. Video pertama dalam folder akan otomatis diputar.
3. Gunakan tombol "Previous" dan "Next" untuk menavigasi video.
4. Klik pada item di playlist untuk memutar video tertentu.
5. Aktifkan mode gelap dengan switch di sebelah kiri video.

### Kode

Berikut adalah kode lengkap untuk proyek ini:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Show Video</title>
    <style>
        *,
        html,
        body {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        .container {
            max-width: 50%;
            margin: 0 auto;
            position: relative;
        }

        .video-component {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
        }

        video {
            display: block;
            width: 100%;
            border: 5px solid crimson;
        }

        .btn {
            border: 0;
            padding: 10px;
            font-weight: 700;
            cursor: pointer;
            font-size: 24px;
            border-radius: 8px;
            opacity: 0.7;
        }

        .btn-next {
            background-color: crimson;
            color: white;
        }

        .btn-prev {
            background-color: #222222;
            color: white;
        }

        .playlist {
            margin-top: 20px;
        }

        .playlist-item {
            cursor: pointer;
            padding: 10px;
            border: 1px solid #ccc;
            margin-bottom: 5px;
        }

        .playlist-item:hover {
            background-color: #f0f0f0;
        }

        .dark-mode {
            background-color: #121212;
            color: white;
        }

        .dark-mode .playlist-item {
            border-color: #444444;
        }

        .dark-mode .playlist-item:hover {
            background-color: #333333;
        }

        .dark-mode video {
            border-color: #444444;
        }

        .dark-mode-toggle {
            display: flex;
            align-items: center;
            margin-top: 20px;
        }

        .dark-mode-toggle input {
            display: none;
        }

        .dark-mode-toggle label {
            cursor: pointer;
            text-align: center;
            padding: 10px;
            color: black;
            margin-left: 10px;
        }

        .dark-mode-toggle input:checked + label {
            color: crimson;
        }

        .switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 34px;
        }

        .switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 34px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 26px;
            width: 26px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: crimson;
        }

        input:checked + .slider:before {
            transform: translateX(26px);
        }
    </style>
</head>

<body>
    <div class="container">
        <input id="folderInput" type="file" webkitdirectory multiple>
        <video id="videoPlayer" width="1080" controls>
            <source id="videoSource" src="" type="video/mp4" />
            Your browser does not support the video tag.
        </video>
        <div class="video-component">
            <button onclick="prevVideo()" class="btn btn-prev">Previous</button>
            <button onclick="nextVideo()" class="btn btn-next">Next</button>
        </div>
        <div class="dark-mode-toggle">
            <label class="switch">
                <input type="checkbox" id="darkModeToggle">
                <span class="slider"></span>
            </label>
            <label for="darkModeToggle">Dark Mode</label>
        </div>
        <div class="playlist" id="playlist"></div>
    </div>

    <script>
        const folderInput = document.getElementById('folderInput');
        const videoPlayer = document.getElementById('videoPlayer');
        const videoSource = document.getElementById('videoSource');
        const playlist = document.getElementById('playlist');
        const darkModeToggle = document.getElementById('darkModeToggle');
        let videoFiles = [];
        let currentIndex = 0;

        folderInput.addEventListener('change', function(event) {
            videoFiles = Array.from(event.target.files).filter(file => file.type.startsWith('video/'));
            videoFiles.sort((a, b) => {
                const aNumber = a.name.match(/\d+/);
                const bNumber = b.name.match(/\d+/);
                return (aNumber ? parseInt(aNumber[0]) : 0) - (bNumber ? parseInt(bNumber[0]) : 0);
            });
            if (videoFiles.length > 0) {
                loadVideo(0);
                updatePlaylist();
            }
        });

        function loadVideo(index) {
            if (index >= 0 && index < videoFiles.length) {
                const fileURL = URL.createObjectURL(videoFiles[index]);
                videoSource.src = fileURL;
                videoPlayer.load();
                currentIndex = index;
            }
        }

        function nextVideo() {
            if (currentIndex < videoFiles.length - 1) {
                loadVideo(currentIndex + 1);
            }
        }

        function prevVideo() {
            if (currentIndex > 0) {
                loadVideo(currentIndex - 1);
            }
        }

        function updatePlaylist() {
            playlist.innerHTML = '';
            videoFiles.forEach((file, index) => {
                const item = document.createElement('div');
                item.className = 'playlist-item';
                item.textContent = file.name;
                item.onclick = () => loadVideo(index);
                playlist.appendChild(item);
            });
        }

        darkModeToggle.addEventListener('change', function() {
            document.body.classList.toggle('dark-mode');
        });
    </script>
</body>

</html>
```

## English Version

This project is an example implementation of a video player with playlist and dark mode features using HTML, CSS, and JavaScript.

### Features

- Play videos from a selected folder.
- Navigate videos with "Previous" and "Next" buttons.
- Clickable video playlist to play specific videos.
- Dark mode toggle switch.

### How to Use

1. Select a folder containing videos by clicking the file input.
2. The first video in the folder will automatically play.
3. Use the "Previous" and "Next" buttons to navigate videos.
4. Click on an item in the playlist to play a specific video.
5. Toggle dark mode with the switch on the left side of the video.

### Code

Here is the complete code for this project:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Show Video</title>
    <style>
        *,
        html,
        body {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        .container {
            max-width: 50%;
            margin: 0 auto;
            position: relative;
        }

        .video-component {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
        }

        video {
            display: block;
            width: 100%;
            border: 5px solid crimson;
        }

        .btn {
            border: 0;
            padding: 10px;
            font-weight: 700;
            cursor: pointer;
            font-size: 24px;
            border-radius: 8px;
            opacity: 0.7;
        }

        .btn-next {
            background-color: crimson;
            color: white;
        }

        .btn-prev {
            background-color: #222222;
           
