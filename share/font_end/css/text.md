# 文本
- 概要：
    - text-indent
    - text-overflow
        - clip
        - ellpsis
    - vertival-align
        - auto
        - baseline
        - sub
        - super
        - top
        - middle
        - bottom
        - length
    - text-align
    - direction
    - white-space
        - normal
        - pre
        - nowrap
        - pre-wrap
        - pre-line
        - inherit
    - word-break
        - normal
        - keep-all
        - break-all
    - word-wrap
        - normal
        - break-word
- 案例：
    ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title> 文本属性 </title>
            <style type="text/css">
                /*
                    - vertival-align
                        - auto
                        - baseline
                        - sub
                        - super
                        - top
                        - middle
                        - bottom
                        - length
                */
                div {
                    border: 1px solid black;
                    height: 30px;
                    width: 200px;
                }

                #gushi {
                    border: 1px solid #000000;
                    height: 80px;
                    width: 240px;
                }

                #wb {
                    border: 1px solid #000000;
                    height: 50px;
                    width: 240px;
                }

                #ww {
                    border: 1px solid #000000;
                    height: 50px;
                    width: 140px;
                }


            </style>
        </head>
        <body>
            <h2>缩进 20pt - text-indent: 20pt</h2>
            <div style="text-indent: 20pt;">测试文字</div>

            <h2>缩进 40pt - text-indent: 40pt;</h2>
            <div style="text-indent: 40pt;">测试文字</div>

            <h2>居中对齐 - text-align: center;</h2>
            <div style="text-align: center;">测试文字</div>

            <h2>居右对齐 - text-align: right;</h2>
            <div style="text-align: right;">测试文字</div>

            <h2>文本从右边流入 - direction: rtl;</h2>
            <div style="direction: rtl;">测试文字</div>

            <h2>文本从左边流入 - direction: ltr;</h2>
            <div style="direction: ltr;">测试文字</div>

            <h2>当文字溢出时，制作简单的裁剪 - overflow: hidden; white-space: nowrap;text-overflow: clip;</h2>
            <div style="overflow: hidden; white-space: nowrap;text-overflow: clip;">读一句古诗，白日依山尽，黄河入海流。欲穷千里目，更上一层楼。</div>

            <h2>当文字溢出时，裁剪之后显示裁剪标记 - overflow: hidden; white-space: nowrap;text-overflow:ellipsis;</h2>
            <div style="overflow: hidden; white-space: nowrap;text-overflow:ellipsis;">读一句古诗，白日依山尽，黄河入海流。欲穷千里目，更上一层楼。</div>

            <h2>忽略文本中的空白、换行符号 - white-space: normal;</h2>
            <div id="gushi" style="white-space: normal;">
                    <<静夜思>>
                床前明月光，疑是地上霜。
                举头望明月，低头思故乡。
            </div>

            <h2>保留文本中的空白、换行符号 - white-space: pre;</h2>
            <div id="gushi" style="white-space:pre;">
                <<静夜思>>
                    床前明月光，疑是地上霜。
                    举头望明月，低头思故乡。
            </div>

            <h2>忽略文本中的空白、换行符号，强制不换行 - white-space: nowrap;</h2>
            <div id="gushi" style="white-space:nowrap;">
                <<静夜思>>
                    床前明月光，疑是地上霜。
                    举头望明月，低头思故乡。
            </div>

            <h2>保留文本中的序列、换行符 - white-space: pre-wrap;; </h2>
            <div id="gushi" style="white-space: pre-wrap;">
                <<静夜思>>
                    床前明月光，   疑是地上霜。
                    举头望明月，   低头思故乡。
            </div>

            <h2>合并文本中空白序列，保留换行符 - white-space: pre-line;</h2>
            <div id="gushi" style="white-space: pre-line;">
                <<静夜思>>
                    床前明月光，   疑是地上霜。
                    举头望明月，   低头思故乡。
            </div>

            <h2>不允许在单词中间换行 word-break: keep-all;</h2>
            <div id="wb">
                The moon in front of the bed is the frost on the ground.Raising my head, I see the moon so bright; withdrawing my eyes, my nostalgia comes around.
            </div>
            <br/>
            <div id="wb" style="word-break: keep-all;">
                The moon in front of the bed is the frost on the ground.Raising my head, I see the moon so bright; withdrawing my eyes, my nostalgia comes around.
            </div>

            <h2>指定允许在单词中换行 - word-break: break-all;</h2>
            <div id="wb" style="word-break: break-all;">
                The moon in front of the bed is the frost on the ground.Raising my head, I see the moon so bright; withdrawing my eyes, my nostalgia comes around.
            </div>

            <h2>不允许在长单词，url地址中间换行</h2>
            <div id="ww" style="word-wrap: normal;">
            ldiognd https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&rsv_idx=1&tn=baidu&wd=%E9%9D%99%E5%A4%9C%E6%80%9D%E5%8F%A4%E8%AF%97&fenlei=256&rsv_pq=e1af8fd40000dc20&rsv_t=cca9q08%2F0OcPOX6Is%2FKm4gJ6RGBZynAK%2FfOEwXaKLdzb8wOor023MdgcRTM&rqlang=cn&rsv_enter=1&rsv_dl=ts_0&rsv_sug3=13&rsv_sug1=18&rsv_sug7=100&rsv_sug2=0&rsv_btype=i&prefixsug=%25E9%259D%2599%25E5%25A4%259C%25E6%2580%259D&rsp=0&inputT=7979&rsv_sug4=7979
            </div>

            <h2>允许在长单词，url地址中间换行</h2>
            <div id="ww" style="word-wrap: break-word;">
            ldiognd https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&rsv_idx=1&tn=baidu&wd=%E9%9D%99%E5%A4%9C%E6%80%9D%E5%8F%A4%E8%AF%97&fenlei=256&rsv_pq=e1af8fd40000dc20&rsv_t=cca9q08%2F0OcPOX6Is%2FKm4gJ6RGBZynAK%2FfOEwXaKLdzb8wOor023MdgcRTM&rqlang=cn&rsv_enter=1&rsv_dl=ts_0&rsv_sug3=13&rsv_sug1=18&rsv_sug7=100&rsv_sug2=0&rsv_btype=i&prefixsug=%25E9%259D%2599%25E5%25A4%259C%25E6%2580%259D&rsp=0&inputT=7979&rsv_sug4=7979
            </div>

        </body>
        </html>

    ```