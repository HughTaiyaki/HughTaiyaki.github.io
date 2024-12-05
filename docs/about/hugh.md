
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
    <title>About Me</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        /* display: flex; */
        /* justify-content: center; */
        /* align-items: center; */
        /* height: 100vh; */
        /* background-color: #f4f4f4; */
      }

      @keyframes rotate-animation {
        0% {
          transform: translate(-50%, -50%) rotate(0deg);
        }
        100% {
          transform: translate(-50%, -50%) rotate(360deg);
        }
      }

      @keyframes avatar-rotate {
        0% {
          transform: rotate(0deg);
        }
        100% {
          transform: rotate(360deg);
        }
      }

      .about-container {
        text-align: center;
        background: #fff;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      }

      .profile-pic {
        position: relative;
        width: 150px;
        height: 150px;
        border-radius: 50%;
        margin: 0 auto;
        padding: 5px;
        border: 2px solid #add8e6;
      }

      .profile-pic img {
        border-radius: 50%;
        width: 100%;
        height: 100%;
        transition: all 1s ease-out;
      }

      .profile-pic:hover img {
        animation: avatar-rotate 2s cubic-bezier(0.68, -0.55, 0.27, 1.55) infinite;
      }

      .container {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 115px;
        height: 115px;
        border-radius: 50%;
        animation: rotate-animation 5s linear infinite;
      }

      .dot {
        width: 10px;
        height: 10px;
        background-color: #007BFF;
        border-radius: 50%;
      }

      .personal-info h2 {
        font-size: 2em;
        margin-top: 10px;
      }

      .personal-info h3 {
        font-size: 1.5em;
        color: gray;
      }

      .links a {
        display: inline-block;
        margin: 10px;
        text-decoration: none;
        font-size: 1.2em;
        color: #333;
      }

      .links a:hover {
        color: #007BFF;
      }

      .footer {
        margin-top: 50px;
        color: gray;
        font-size: 0.9em;
      }
    </style>
  </head>
  <body>
    <div class="about-container">
      <div class="profile-pic">
        <img src="../../img/favicon.png" alt="Profile Picture">
        <div class="container">
          <div class="dot"></div>
        </div>
      </div>
      <div class="personal-info">
        <h2>HughTaiyaki</h2>
        <h3>鲷鱼烧</h3>
      </div>
      <div class="links">
        <a href="https://github.com/HughTaiyaki">
          <i class="fab fa-github"></i>
        </a>
        <a href="https://hughtaiyaki.github.io/Blog/">
          <i class="fas fa-blog"></i>
        </a>
        <a href="https://hughtaiyaki.github.io/">
          <i class="fas fa-book"></i>
        </a>
        <a href="https://space.bilibili.com/38913631">
          <i class="fas fa-play-circle"></i>
        </a>
        <a href="mailto:xcy.231x@gmail.com">
          <i class="fas fa-envelope"></i>
        </a>
        <a href="https://yourtelegramurl.com">
          <i class="fab fa-telegram"></i>
        </a>
      </div>
      <div class="footer">
        <p>Copyright © 2022-2024 @HughTaiyaki</p>
      </div>
    </div>
  </body>
</html>
