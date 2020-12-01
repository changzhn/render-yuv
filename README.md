# 如何使用WebGL渲染YUV数据

## 1.0 什么是YUV

1.1 YUV的解释可以看[如何理解 YUV ？](https://zhuanlan.zhihu.com/p/85620611)；

1.2 为什么要使用YUV数据：因为视频或者图片的raw data就是yuv格式的，如果要使用canvas渲染视频或者图片就需要渲染YUV。
其实YUV可以直接转成RGB来渲染，但是需要消耗CPU，而使用WebGL来转可以调用GPU，从而减轻CPU的压力；

1.3 如何获取YUV数据：正常来说视频解码后的帧数据就是YUV。本例为了测试，就使用了ffmpeg将图片转成YUV来模拟视频的一帧；

```bash
cd assets
ffmpeg -i 1920_1080.jpg -s 1920x1080 -pix_fmt yuv420p 002.yuv
# 如果存在的话，会提醒要不要覆盖
```

这样就得到了YUV的数据，可以使用ffplay检查一下数据是否正确

```
ffplay -f rawvideo -video_size 1920x1080 -pix_fmt yuv420p 1920_1080.yuv
```

## 2.0 demo1

渲染方法是直接从附录中的文章中拿过来的，目前对WebGL也不太熟悉（拿来主义：拿过来好好学习）；
`renderImg`方法是需要宽高参数的，正常应该是从解复用中得到宽高参数的，这里就直接写成固定值

## x. 附录

- [IVWEB 玩转 WASM 系列-WEBGL YUV渲染图像实践](https://zhuanlan.zhihu.com/p/94527880)

- [FFmpeg下载](https://ffmpeg.org/download.html)

- [FFmpeg 视频处理入门教程](https://www.ruanyifeng.com/blog/2020/01/ffmpeg.html)