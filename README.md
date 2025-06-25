# HollywoodTamilan
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Movie Streaming Website</title>
  <link rel="stylesheet" href="style.css">
  <style>
    /* Basic Reset */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: Arial, sans-serif;
    background-color: #141414;
    color: #fff;
  }
  
  header {
    text-align: center;
    padding: 20px;
    background: #000;
  }
  
  h1 {
    color: #e50914;
  }
  
  /* Movie Gallery */
  #gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
    padding: 20px;
  }
  
  .movie img {
    width: 100%;
    height: auto;
    cursor: pointer;
    border-radius: 10px;
  }
  
  /* Modal */
  .modal {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.8);
    justify-content: center;
    align-items: center;
  }
  
  .modal-content {
    background: #222;
    padding: 20px;
    border-radius: 8px;
    text-align: center;
    max-width: 400px;
    width: 100%;
  }
  
  .modal-content h2 {
    color: #e50914;
  }
  
  .modal-content button {
    background: #e50914;
    border: none;
    padding: 10px 20px;
    margin-top: 20px;
    cursor: pointer;
    border-radius: 5px;
    color: #fff;
  }
  
  .close {
    position: absolute;
    top: 10px;
    right: 10px;
    cursor: pointer;
    font-size: 24px;
  }
  
  /* Player */
  .player {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.9);
    justify-content: center;
    align-items: center;
  }
  
  .player video {
    max-width: 80%;
    max-height: 80%;
  }
  
  .control-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    background: #e50914;
    color: #fff;
    padding: 10px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
  }
  
  </style>
</head>
<body>
  <!-- Header -->
  <header>
    <h1>HOLLYWOOD TAMILAN</h1>
  </header>

  <!-- Movie Gallery -->
  <section id="gallery">
    <div class="movie" onclick="showDetails('Movie 1', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $1,024,583,854', 'moviehp1.mp4')">
      <img src="hp1.jpg" alt="Movie 1">
    </div>
    <div class="movie" onclick="showDetails('Movie 2', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $882,545,819', 'moviehp2.mp4')">
      <img src="hp2.jpg" alt="Movie 2">
    </div>
    <div class="movie" onclick="showDetails('Movie 3', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $808,485,294', 'moviehp3.mp4')">
      <img src="hp3.jpg" alt="Movie 3">
    </div>
    <div class="movie" onclick="showDetails('Movie 4', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $897,468,952', 'moviehp4.mp4')">
      <img src="hp4.jpg" alt="Movie 4">
    </div>
    <div class="movie" onclick="showDetails('Movie 1', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $942,861,168', 'moviehp5.mp4')">
        <img src="hp5.jpg" alt="Movie 1">
      </div>
      <div class="movie" onclick="showDetails('Movie 2', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $941,055,851', 'moviehp6.mp4')">
        <img src="hp6.jpg" alt="Movie 2">
      </div>
      <div class="movie" onclick="showDetails('Movie 3', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $1.342 billion', 'moviehp7.mp4')">
        <img src="hp7.jpg" alt="Movie 3">
      </div>
      <div class="movie" onclick="showDetails('Movie 4', 'Cast: Daniel Radcliffe,Emma Watson,Rupert Grint', 'Box Office: $1.342 billion', 'moviehp8.mp4')">
        <img src="hp8.jpg" alt="Movie 4">
      </div>
    <!-- Add more movie posters as needed with unique details -->
  </section>

  <!-- Movie Details Modal -->
  <div id="modal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeModal()">&times;</span>
      <h2 id="movieTitle"></h2>
      <p id="movieCast"></p>
      <p id="movieBoxOffice"></p>
      <button onclick="playMovie()">Watch Movie</button>
    </div>
  </div>

  <!-- Movie Player -->
  <div id="player" class="player">
    <video id="videoPlayer" controls>
      <source id="videoSource" type="video/mp4">
      Your browser does not support the video tag.
    </video>
    <button class="control-btn" onclick="closePlayer()">Close</button>
  </div>

  <script>
    // Store the current movie source to be played
let currentMovieSource = '';

// Show movie details modal with dynamic content
function showDetails(title, cast, boxOffice, movieSource) {
  document.getElementById('movieTitle').innerText = title;
  document.getElementById('movieCast').innerText = cast;
  document.getElementById('movieBoxOffice').innerText = boxOffice;
  currentMovieSource = movieSource; // Store the movie source for playback
  document.getElementById('modal').style.display = 'flex';
}

// Close movie details modal
function closeModal() {
  document.getElementById('modal').style.display = 'none';
}

// Play the selected movie in the player
function playMovie() {
  document.getElementById('modal').style.display = 'none';
  document.getElementById('player').style.display = 'flex';
  const video = document.getElementById('videoPlayer');
  document.getElementById('videoSource').src = currentMovieSource;
  video.load(); // Load the new video source
  video.play();
}

// Close the player and stop the video
function closePlayer() {
  const video = document.getElementById('videoPlayer');
  video.pause();
  video.currentTime = 0;
  document.getElementById('player').style.display = 'none';
}

  </script>
</body>
</html>
