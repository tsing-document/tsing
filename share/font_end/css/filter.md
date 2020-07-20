# 滤镜
- 概要：
    - blur(Npx)
    - brightness(百分比)
    - contrast(百分比)
    - drop-shadow(xoffset, yoffset, redius, color)
    - grayscale
    - hue-rotate(Ndeg)
    - invert(百分比)
    - opacity(百分比)
    - saturate(百分比)
    - sepia(百分比)
- 语法：
- 案例：
    ```css
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>滤镜</title>
            <style type="text/css">
                div {
                    float: left;
                }

                img{
                    width: 300px;
                    height: 300px;
                }
            </style>
        </head>
        <body>
            <div>
                <h2>原始图片</h2>
                <img src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg" alt="万茜"/>
            </div>

            <div>
                <h2>blur</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: blur(10px);"/>
            </div>
                
            <div>
                <h2>brightness</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: brightness(40%);"/>
            </div>
            
            <div>
                <h2>contrast</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: contrast(40%);"/>
            </div>
            
            <div>
                <h2>drop-shadow</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: drop-shadow(8px 8px 10px red);"/>
            </div>

            <div>
                <h2>grayscale</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: grayscale(50%);"/>
            </div>
            
            <div>
                <h2>hue-rotate</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: hue-rotate(20deg);"/>
            </div>

            <div>
                <h2>invert</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: invert(40%);"/>
            </div>

            <div>
                <h2>opacity</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: opacity(30%);"/>
            </div>

            <div>
                <h2>saturate</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: saturate(30%);"/>
            </div>

            <div>
                <h2>sepia</h2>
                <img
                    src="https://imgs.tom.com/ent/201811/CONTENT3C54361E743B4AD5.jpg"
                    alt="万茜"
                    style="filter: sepia(30%);"/>
            </div>
        </body>
        </html>
    ```
