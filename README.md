# Simple-guide2tesseract-ocr
An easy to understand guide to using tesseract-ocr for beginners through hands-on examples. <br><br>

<h3>Installation of tesseract-ocr</h3><br>
<p> Install Google Tesseract OCR, Under Debian/Ubuntu you can use the package tesseract-ocr.
<pre>
  $ sudo apt install tesseract-ocr 
  $ sudo apt install libtesseract-dev 
 </pre>
</p>
<br>

<p>
Training Tools
<pre>
$ sudo apt-get install libicu-dev
$ sudo apt-get install libpango1.0-dev
$ sudo  apt-get install libcairo2-dev
</pre>
</p>
<br>

<p>
To finish the setup, we need to make our tools, so go into the Tesseract directory (by default named tessdata), then execute the following commands:
<pre>
$ make
$ make training
$ make training-install
</pre>
</p>
<br>
 
<hr>

<h3>Optional</h3>
<p>
Install pytesseract (the Python bindings used to interface with Tesseract) 
Prerequisites: <br>
Python(3.6+), <br>
Python Imaging Library(fork) - https://pypi.org/project/Pillow/ <br>
</p>
<br>

<p>
Installing pytesseract from source:
<pre>
$ git clone https://github.com/madmaze/pytesseract.git
$ cd pytesseract && pip install -U .
</pre>
</p>
<br>

<p>
To check the path of pytesseract and pillow
<pre>
$ dpkg -L tesseract-ocr
$ dpkg -L pillow
</pre>
</p>
<br>

<p>
Testing:
<pre>
pip install tox ( https://pypi.org/project/tox/ )
</pre>
</p>
<br>

<p>
Type tox in terminal
<pre>
$ tox
</pre>
</p>
<br>

<p>
How to start with tox <br>
source - https://manpages.ubuntu.com/manpages/eoan/man1/tox.1.html <br>
Refer to RELATED PROJECTS section in the above source.
</p>
</section>

<hr>

<h3>Image preprocessing tools to improve quality of image </h3>
<p>
Refer to Source for additional information - https://tesseract-ocr.github.io/tessdoc/ImproveQuality.html#tools--libraries </p><br>
<p>
 Installation of ImageMagick and scantailor advanced tools </p>
 <p>
  First install git
  <pre>
  $ sudo apt install git
  $ Sudo apt install pkg-config
  </pre>
 </p> 
<br>

<p>
Download ImageMagick.tar.gz from https://download.imagemagick.org/ImageMagick/download/ImageMagick.tar.gz and extract it to any folder.</p>
<br>

<p>
To configure, type: 
<pre>
$ cd ImageMagick-7.0.11
$ ./configure
$ make
</pre>
</p>  
<br>

<p>
  Administrator privileges are required to install. To install, type 
  <pre>
sudo make install
</pre>
</p>
<br>

<p>
  You may need to configure the dynamic linker run-time bindings: 
 <pre>
sudo ldconfig /usr/local/lib
</pre>
</p>
<br>

<p>
  Finally, to verify if the ImageMagick install works properly, type
<pre>
/usr/local/bin/convert logo: logo.gif
</pre>
<br>

<p>
  Run this command to check installation
  <pre>
  make check
  </pre>
</p>
<br>

<p> 
  The result should appear like this 
  <pre>
Testsuite summary for ImageMagick 7.0.11-4
============================================================================
# TOTAL: 86
# PASS:  86
# SKIP:  0
# XFAIL: 0
# FAIL:  0
# XPASS: 0
# ERROR: 0
============================================================================
  </pre>
  </p>
  <br>
  
<p>
  <b> Install scantailor advanced</b><br>
  source - https://snapcraft.io/install/scantailor-advanced/ubuntu
</p>
<br>

<p><em>
  Note - Raw scanned images requires image preprocessing processes like Grayscaling, Thresholding, Noise removal, Deskewing(rotation), etc. This stage might become difficult for Beginners. Using Digital images to learn tesseract-ocr command line would be fine at the initial stage.
  </em>
</p>
<br>
<hr>

<h3> Command-line tutorial</h3>
<p>Refer to source - Refer to source - https://github.com/tesseract-ocr/tesseract/blob/master/doc/tesseract.1.asc 
</p>
<br>

<p>
In/Out statements <br>
FILE - name of the input file <br>
OUTBASE - basename of the output file. Default - (.txt, .pdf, .tif, etc) <br>
OPTIONS <br>
CONFIGFILE - config files include OUTPUTBASE.xml, OUTPUT.pdf, OUTPUT. <br>
  <em>NOTE - The Options --psm N, -l lang, -l script should occur before a CONFIGFILE </em>
</p> 
<br>

<p> To output text in terminal
<pre>
$ tesseract -dir PATH FILE stdout
$ tesseract /home/username/testimages/image.jpg stdout
</pre>
</p>
<br>

<p> To output only digits in terminal
<pre>
$ tesseract -dir PATH FILE stdout digits
$ tesseract testimages/image.jpg stdout digits
</pre>
</p>
<br>

<p> To save output image in a folder(ex: outputs) 
<pre>
$ tesseract -dir PATH FILE (output) -dir PATH FILE 
$ tesseract testimages/image.jpg outputs/finalimage.jpg 
</pre>
</p>
<br>

<p> To save output by default in a text file <br> 
<code>
  $ tesseract -dir PATH FILE OUTPUTBASE
</code> <br>
  (by specifying .txt, .pdf, .xml, you can store file in desired format) <br>
  <code> 
    $ tesseract testimages/image.jpg OUTPUTBASE
  </code><br>
  File is saved in home folder
</p>
<br>

<p> To save output in a file in a folder <br>
<code>
$ tesseract -dir PATH FILE (output) -dir PATH file.txt
  </code> <br>
<code>
$ tesseract testimages/image.png outputs/finalimage.txt
  </code> <br>
You can save file in any format(txt, pdf, jpg, png, xml)
</p>
<br>

<p> To output test in a image using -l lang
<pre>
$ tesseract -dir PATH FILE -l lang stdout
$ tesseract testimages/image.jpg stdout -l eng
</pre>
</p>
<br>

<p> To use page segmentation mode(--psm N) <br>
<code>
$ tesseract testimages/image.jpg stdout -l eng --psm 1 
</code> <br>
(Try --psm 0, --psm 1, --psm 2, --psm 4, --psm 6, --psm 11, --psm 12)
</p>
<br>

<p>  
https://github.com/tesseract-ocr/tessdata is a 3rd repo that has models which support both the Tesseract 3 legacy OCR engine and the Tesseract 4 LSTM OCR engine.
<br><br>
 Both tessdata_fast - https://github.com/tesseract-ocr/tessdata_fast/tree/master/script  and tessdata_best - https://github.com/tesseract-ocr/tessdata_best/tree/master/script  only support the LSTM OCR engine. 
</p>
<br>

<p>  
 For this tutorial, sanskrit, hindi languages traineddata files are downloaded manually  from repository  https://github.com/tesseract-ocr/tessdata 
</p>
<br>

<p> Open terminal, navigate to downloads section. To move download files to tessdata directory in your system <br>  
<code>
$ sudo mv san.traineddata /usr/share/tesseract-ocr/4.00/tessdata
</code> <br>
or you can move to tessdata directory <br>
<code>
$ sudo wget https://github.com/tesseract-ocr/tessdata/blob/master/eng.traineddata
</code> <br>
(replace eng with any languages you need to download)
</p>
<br>

<p><em> Note: Use --oem 1 for Indic and Arabic scripts</em> <br>
  To run any trained data file TESSDATA_PREFIX environment variable should be set to your "tessdata" directory. <br>
  Determine the full system path to tessdata directory from tessdata  <br>
<code>
$ pwd
</code> <br>
  Result in ubuntu:<code>$ /usr/share/tesseract-ocr/4.00/tessdata</code>
</p>
<br>

<p> From tessdata directory, Set the TESSDATA_PREFIX environment variable to point to your tessdata directory, thereby allowing Tesseract to find the language packs. 
<pre>
$ export TESSDATA_PREFIX=/usr/share/tesseract-ocr/4.00/tessdata
</pre>
</p>
<br>

<p> While executing commands after this step, if your directory path, or image format or tessdata directory path is wrong or mistyped, you would get this error.
<pre>
Error opening data file TESSDATA_PREFIX/eng.traineddata
Please make sure the TESSDATA_PREFIX environment variable is set to your "tessdata" directory.
Failed loading language 'eng'
Tesseract couldn't load any languages!
Could not initialize tesseract.
</pre>
</p>
<br>

<p><em>
  Note - Download digital images of the language that you intend to use tesseract OCR on.</em>
</p>
<br>

<p> Using san.traineddata(sanskrit language) 
<pre>
$ tesseract /home/username/testimages/deva_sans.jpg stdout --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata -l san --oem 1 --psm 4
</pre>
</p>
<br>

<p> $ tesseract /testimages/deva_sans.jpg stdout --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata/scripts -l Devanagari --oem 1 --psm 4 <br>
  OPTION: -dpi N - N is value, atleast 300 <pre>
$ tesseract /testimages/testimage_multi2.png stdout --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata -l eng+kan+ben+tam+tel+hin --oem 1 --psm 11 --dpi 300
</pre>
</p>
<br>

<p> To use scripts, download the scripts from tessdata and move them to scripts folder in tessdata directory.  
<pre>
$ tesseract /testimages/deva_sans.jpg stdout --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata/scripts -l Devanagari --oem 1 --psm 4
</pre>
</p>
<br>

<p> To output after whitelisting characters characters <br>
  OPTION: -c  - give CONFIGVAR parameter multiple  arguments
<pre>
$ tesseract testimage_eng5.png stdout -l eng --psm 6 -c tessedit_char_whitelist=abcdefghijklmnopqrstuvwxyz
</pre>
</p>
<br>

<p> Using -c tessedit_char_whitelist and output text file to a desired location
<pre>
$ tesseract /home/username/testimages/testimage_eng3.jpg /home/username/outputs/testimage_eng3_whitelist --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata --dpi 300  -l eng -c tessedit_char_whitelist=abcdefghijklmnopqrstuvwxyz --oem 1 --psm 4 txt
</pre>
</p>
<br>

<p> Using -c tessedit_char_blacklist and output text file to a desired location
<pre> 
$ tesseract /home/username/testimages/testimage_eng3.jpg /home/username/testimage_eng3_blacklist --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata --dpi 300  -l eng -c tessedit_char_blacklist=abcdefghijklmnopqrstuvwxyz --oem 1 --psm 4 txt
</pre>
</p>
<br>

<p>
  Source - https://tesseract-ocr.github.io/tessdoc/Command-Line-Usage
</p>
<br>

<p>
  <em>NOTE - The Options --psm N, -l lang, -l script should occur before a CONFIGFILE
</em>
</p>
<br>

<p>To create searchable pdf <br>
  To create a pdf with the image and a separate searchable text layer with the recognized text. 
<pre>
$ tesseract /home/username/testimages/deva_sans.png /home/username/outputs/devanagari_sans  --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata -l san --oem 1 --psm 4 pdf
</pre>
</p>
<br>

<p> HOCR output <br>
  Use ???hocr??? config file by adding hocr at the end of the command to get the HOCR    output.
<pre>
$ tesseract /home/username/testimages/deva_sans.png /home/username/outputs/devanagari_sans  --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata -l san --oem 1 --psm 4 hocr
</pre>
</p>
<br>

<p> TSV output 
<pre>
$ tesseract /home/username/testimages/deva_sans.png /home/username/outputs/devanagari_sans  --tessdata-dir /usr/share/tesseract-ocr/4.00/tessdata -l san --oem 1 --psm 4 tsv
</pre>
</p>
<br>
 
 
<!--
<p>  
<pre>
</pre>
</p>
<br> -->
