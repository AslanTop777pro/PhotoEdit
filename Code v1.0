from PyQt5.QtCore import Qt
import os
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QLabel, QVBoxLayout,QHBoxLayout ,QRadioButton,QMessageBox, QGroupBox,QButtonGroup, QLineEdit, QTextEdit, QListWidget,QInputDialog, QFileDialog
from PyQt5.QtGui import * 
from PIL import Image
from PIL import ImageFilter
app = QApplication([])
workdir = ''
main_win = QWidget()
main_win.resize(700,600)
dir_but = QPushButton('Папка')
img_list = QListWidget()
picture1 = QLabel('Картинка')
leftbut = QPushButton('Лево')
rightbut = QPushButton('Право')
mirrorbut = QPushButton('Зеркало')
blurbut = QPushButton('Резкость')
bwbut = QPushButton('Ч/Б')
hline = QHBoxLayout()
hline1 = QHBoxLayout()
vline = QVBoxLayout()
vline1 = QVBoxLayout()
vline.addWidget(dir_but)
vline.addWidget(img_list)
hline1.addWidget(leftbut)
hline1.addWidget(rightbut)
hline1.addWidget(mirrorbut)
hline1.addWidget(blurbut)
hline1.addWidget(bwbut)
vline1.addWidget(picture1)
vline1.addLayout(hline1)
hline.addLayout(vline)
hline.addLayout(vline1)
main_win.setLayout(hline)
def chooseWorkdir():
    global workdir
    workdir = QFileDialog.getExistingDirectory()
def filter(files, extensions):
    result = list()
    for filename in files:
        for extension in extensions:
            if filename.endswith(extension):
                result.append(filename)
    return result
def showfilenamelist():
    chooseWorkdir()
    extensions = ['.jpg','.png','svg','.jpeg','.gif']
    files = os.listdir(workdir)
    results = filter(files, extensions)
    for result in results:
        img_list.addItem(result)
class ImageProcessor():
    def __init__(self):
        self.picture = None
        self.filename = None
        self.folder = "Folder1"
    def loadImage(self, filename):
        self.filename = filename
        image_path = os.path.join(workdir, filename)
        self.picture = Image.open(image_path)
        pixmapimage = QPixmap()
    def showImage(self, path):
        picture1.hide()
        pixmapimage = QPixmap(path)
        w, h = picture1.width(), picture1.height()
        pixmapimage = pixmapimage.scaled(w,h, Qt.KeepAspectRatio)
        picture1.setPixmap(pixmapimage)
        picture1.show()
    def do_bw(self):
        self.picture = self.picture.convert('L')
        self.saveImage()
        image_path = os.path.join(workdir, self.folder, self.filename)
        self.showImage(image_path)

    def saveImage(self):
        path = os.path.join(workdir, self.folder)
        if not(os.path.exists(path) or os.path.isdir(path)):
            os.mkdir(path)
        image_path = os.path.join(path, self.filename)
        self.picture.save(image_path)

    def do_left(self):
        self.picture = self.picture.rotate(90)
        self.saveImage()
        image_path = os.path.join(workdir, self.folder, self.filename)
        self.showImage(image_path)
    def do_right(self):
        self.picture = self.picture.rotate(270)
        self.saveImage()
        image_path = os.path.join(workdir, self.folder, self.filename)
        self.showImage(image_path)
    def do_mirror(self):
        self.picture = self.picture.transpose(Image.FLIP_LEFT_RIGHT)
        self.saveImage()
        image_path = os.path.join(workdir, self.folder, self.filename)
        self.showImage(image_path)
    def do_blur(self):
        self.picture = self.picture.filter(ImageFilter.SHARPEN)
        self.saveImage()
        image_path = os.path.join(workdir, self.folder, self.filename)
        self.showImage(image_path)


def showChosenImage(self):
    if img_list.currentRow() >= 0:
        filename = img_list.currentItem().text()
        image1.loadImage(filename)
        image_path = os.path.join(workdir, image1.filename)
        image1.showImage(image_path)
 
image1 = ImageProcessor()
img_list.currentRowChanged.connect(showChosenImage)
bwbut.clicked.connect(image1.do_bw)
leftbut.clicked.connect(image1.do_left)
rightbut.clicked.connect(image1.do_right)
mirrorbut.clicked.connect(image1.do_mirror)
blurbut.clicked.connect(image1.do_blur)
dir_but.clicked.connect(showfilenamelist)
main_win.setStyleSheet('''background-color: #1d3352  ; color: #0e8a75''')
main_win.show()
app.exec()
