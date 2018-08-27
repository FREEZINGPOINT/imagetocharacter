# imagetocharacter
将图片转化为字符进行显示


package com.xinan.agent;

import org.junit.Test;

import javax.imageio.ImageIO;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.FileInputStream;
import java.io.FileOutputStream;

/**
 * @author :breakpoint/赵立刚
 * @date : 2018/08/27 15:23:11
 */
public class BufferedInamgeTest {


    String filepath = "/Users/breakpoint/Downloads/4.jpg";
    String outpath = "/Users/breakpoint/Downloads/out.txt";

    char[] chararray = {' ', '.', '!', '*', '@', '\\', ')', '0', ',', '=', '7', '[', ']', '7', '9', '-', 'r', 'g', 'b', 'q', 'v', ',', '7', '6', '7', '6', ')', '0', ',', '='};

    @Test
    public void a() throws Exception {

        FileInputStream fileInputStream = new FileInputStream(filepath);
        BufferedImage read1 = ImageIO.read(fileInputStream);

        FileOutputStream fileOutputStream = new FileOutputStream(outpath, true);

        int width = read1.getWidth();

        System.out.println(width);
        int wDtep = width / 170;


        System.out.println(wDtep);
        int height = read1.getHeight();

        int hDtep = height / 350;

        for (int i = 0; i < width; ) {
            for (int j = 0; j < height; ) {
                int rgb = read1.getRGB(i, j);
                Color color = new Color(rgb);
                int red = color.getRed();
                int blue = color.getBlue();
                int green = color.getGreen();
                int gray = ((red * 30 + blue * 59 + green * 11 + 50) / 2500);
                System.out.println(gray);
                fileOutputStream.write(chararray[gray]);
                //fileOutputStream.write(' ');
                //System.out.print((char) gray);
                j = j + hDtep;
            }
            i = i + wDtep;
            fileOutputStream.write('\r');
            fileOutputStream.write('\n');
            //fileOutputStream.write('\r');
            //fileOutputStream.write('\n');
        }
        fileInputStream.close();
        fileOutputStream.close();
    }
}


