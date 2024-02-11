## webpack-bundle-analyzer插件
作用：可视化地分析打包生成的资源文件，以便更好地理解打包结果，并找出可能存在的优化空间。
- stat size:指的是模块在打包后的大小，即未经过压缩和优化的原始大小。
- parsed size: 指的是模块经过 webpack 解析后的大小，即 webpack 真正会处理的大小，包括了模块间的依赖关系。
- gzipped size:gzip压缩后大小

