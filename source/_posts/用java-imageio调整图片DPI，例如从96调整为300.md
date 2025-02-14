---
title: 用java imageio调整图片DPI，例如从96调整为300
date: 2025-02-13 16:01:03
tags:
- java
- dpi
---

# 用java imageio调整图片DPI，例如从96调整为300 - 古语云 - 博客园

> ## Excerpt
> 因项目需求把图片的DPI值提升到300，否则OCR识别产生错乱：直接上源码：1、图片处理接口： 2、JEPG图片的实现类 3、PNG图片的实现类

---
`package` `util.image.dpi;`

`import` `java.awt.image.BufferedImage;`

`import` `java.io.ByteArrayOutputStream;`

`import` `java.io.IOException;`

`import` `java.net.MalformedURLException;`

`import` `java.util.Iterator;`

`import` `javax.imageio.IIOImage;`

`import` `javax.imageio.ImageIO;`

`import` `javax.imageio.ImageTypeSpecifier;`

`import` `javax.imageio.ImageWriteParam;`

`import` `javax.imageio.ImageWriter;`

`import` `javax.imageio.metadata.IIOInvalidTreeException;`

`import` `javax.imageio.metadata.IIOMetadata;`

`import` `javax.imageio.metadata.IIOMetadataNode;`

`import` `javax.imageio.stream.ImageOutputStream;`

`/**`

 `* PNG图片的实现类`

 `* @author jffan`

 `*`

 `*/`

`public` `class` `PngDPIProcessor` `implements` `ImageDPIProcessor {`

    `/**`

     `* 1英寸是2.54里面`

     `*/`

    `private` `static` `final` `double` `INCH_2_CM =` `2``.54d;`

    `/**`

     `* 根据文件后缀扩展名判断是否能进行处理`

     `* @param fileName`

     `* @return`

     `*/`

    `@Override`

    `public` `boolean` `canHandle(String fileName) {`

        `assert` `fileName !=` `null` `:` `"fileName should not be null"``;`

        `return` `fileName.endsWith(``"png"``) || fileName.endsWith(``"PNG"``);`

    `}`

    `/**`

     `* 处理图片，设置图片DPI值`

     `* @param path`

     `* @param dpi dot per inch`

     `* @return`

     `* @throws IOException`

     `*/`

    `@Override`

    `public` `byte``[] process(BufferedImage image,` `int` `dpi)` `throws` `MalformedURLException, IOException {`

        `for` `(Iterator<ImageWriter> iw = ImageIO.getImageWritersByFormatName(``"png"``); iw.hasNext();) {`

            `ImageWriter writer = iw.next();`

            `ImageWriteParam writeParam = writer.getDefaultWriteParam();`

            `ImageTypeSpecifier typeSpecifier = ImageTypeSpecifier.createFromBufferedImageType(BufferedImage.TYPE_INT_RGB);`

            `IIOMetadata metadata = writer.getDefaultImageMetadata(typeSpecifier, writeParam);`

            `if` `(metadata.isReadOnly() || !metadata.isStandardMetadataFormatSupported()) {`

                `continue``;`

            `}`

            `ByteArrayOutputStream output =` `new` `ByteArrayOutputStream();`

            `ImageOutputStream stream =` `null``;`

            `try` `{`

                `setDPI(metadata, dpi);`

                `stream = ImageIO.createImageOutputStream(output);`

                `writer.setOutput(stream);`

                `writer.write(metadata,` `new` `IIOImage(image,` `null``, metadata), writeParam);`

            `}` `finally` `{`

                `try` `{`

                    `stream.close();`

                `}` `catch` `(IOException e) {`

                `}`

            `}`

            `return` `output.toByteArray();`

        `}`

        `return` `null``;`

    `}`

    `/**`

     `* 设置图片的DPI值`

     `* @param metadata`

     `* @param dpi`

     `* @throws IIOInvalidTreeException`

     `* @author 范继峰`

     `* @date 2019年7月30日上午10:53:18`

     `* @return void`

     `*/`

    `private` `void` `setDPI(IIOMetadata metadata,` `int` `dpi)` `throws` `IIOInvalidTreeException {`

        `double` `dotsPerMilli =` `1.0` `* dpi /` `10` `/ INCH_2_CM;`

        `IIOMetadataNode horiz =` `new` `IIOMetadataNode(``"HorizontalPixelSize"``);`

        `horiz.setAttribute(``"value"``, Double.toString(dotsPerMilli));`

        `IIOMetadataNode vert =` `new` `IIOMetadataNode(``"VerticalPixelSize"``);`

        `vert.setAttribute(``"value"``, Double.toString(dotsPerMilli));`

        `IIOMetadataNode dim =` `new` `IIOMetadataNode(``"Dimension"``);`

        `dim.appendChild(horiz);`

        `dim.appendChild(vert);`

        `IIOMetadataNode root =` `new` `IIOMetadataNode(``"javax_imageio_1.0"``);`

        `root.appendChild(dim);`

        `metadata.mergeTree(``"javax_imageio_1.0"``, root);`

    `}`

`}`
