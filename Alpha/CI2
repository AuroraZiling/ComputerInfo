import sys
import subprocess
from PyQt5.QtWidgets import QApplication, QLineEdit, QLabel, QWidget, QPushButton
from PyQt5.QtWidgets import QHBoxLayout, QVBoxLayout, QDialog
from PyQt5.QtCore import Qt


class MainForm(QWidget):
    def __init__(self):
        super(MainForm, self).__init__()
        self.resize(250, 200)
        self.setWindowTitle("CI")
        self.setFixedSize(self.width(), self.height())

        self.intro_label = QLabel("Computer Information", self)
        self.cpu_button = QPushButton("查看CPU信息", self)
        self.graphics_button = QPushButton("查看显卡信息", self)
        self.memory_button = QPushButton("查看内存信息", self)
        self.disk_button = QPushButton("查看硬盘信息", self)

        self.all_v_layout = QVBoxLayout()
        self.all_v_layout.addWidget(self.intro_label)
        self.all_v_layout.addWidget(self.cpu_button)
        self.all_v_layout.addWidget(self.graphics_button)
        self.all_v_layout.addWidget(self.memory_button)
        self.all_v_layout.addWidget(self.disk_button)
        self.setLayout(self.all_v_layout)

        self.cpuPage = CPU()
        self.labelInit()
        self.buttonInit()

    def show_cpuPage(self):
        self.cpuPage.exec_()

    def labelInit(self):
        self.intro_label.setAlignment(Qt.AlignCenter)

    def buttonInit(self):
        self.cpu_button.clicked.connect(self.show_cpuPage)
        self.graphics_button.clicked.connect(self.graphicsInfo)
        self.memory_button.clicked.connect(self.memoryInfo)
        self.disk_button.clicked.connect(self.diskInfo)

    def graphicsInfo(self):
        pass

    def memoryInfo(self):
        pass

    def diskInfo(self):
        pass


class CPU(QDialog):
    def __init__(self):
        super(CPU, self).__init__()
        self.cpuName = subprocess.Popen("wmic cpu get name", shell=True, stdout=subprocess.PIPE, bufsize=-1)
        self.cpuNameStdout = str(self.cpuName.communicate()[0]).split('\\n')[1].split('\\r')[0].split('@')
        self.cpuCore = subprocess.Popen("wmic cpu get NumberOfCores", shell=True, stdout=subprocess.PIPE, bufsize=-1)
        self.cpuCoreStdout = str(self.cpuCore.communicate()[0]).split('\\n')[1].replace('\\r', '').replace(' ', '')
        self.cpuThread = subprocess.Popen("wmic cpu get NumberOfLogicalProcessors", shell=True, stdout=subprocess.PIPE,
                                          bufsize=-1)
        self.cpuThreadStdout = str(self.cpuThread.communicate()[0]).split('\\n')[1].replace('\\r', '').replace(' ', '')
        self.cpuGhz = self.cpuNameStdout[-1][1:].strip()
        self.cpuNameStdout = self.cpuNameStdout[0].replace("CPU", '').strip()
        self.cpuBrand = "AMD®"
        if "Intel" in self.cpuNameStdout:
            self.cpuBrand = "英特尔®"
            if "Core" in self.cpuNameStdout:
                self.cpuBrand += " 酷睿™系列"
                tmp = self.cpuNameStdout.split('-')[1].split()[0]
                self.mayPlatForm = ""
                self.showOther = 1
                if 'H' in tmp:
                    self.cpuType = "标压CPU"
                    self.mayPlatForm = "笔记本"
                elif 'U' in tmp:
                    self.cpuType = "低压CPU"
                    self.mayPlatForm = "笔记本"
                elif 'K' in tmp:
                    self.cpuType = "不锁倍频（可超频）CPU"
                    self.mayPlatForm = "台式机"
                elif 'S' in tmp:
                    self.cpuType = "65W低功耗CPU"
                    self.mayPlatForm = "笔记本"
                elif 'T' in tmp:
                    self.cpuType = "45W节能CPU"
                    self.mayPlatForm = "笔记本"
                elif 'M' in tmp:
                    self.cpuType = "35W双核CPU"
                    self.mayPlatForm = "笔记本"
                elif 'QM' in tmp:
                    self.cpuType = "45W四核CPU"
                    self.mayPlatForm = "笔记本"
                elif 'XM' in tmp:
                    self.cpuType = "至尊版"
                    self.mayPlatForm = "笔记本"
                elif 'F' in tmp:
                    self.cpuType = "无核显CPU"
                    self.mayPlatForm = "台式机"
            elif "Pentium" in self.cpuNameStdout:
                self.cpuBrand += " 奔腾™系列"
            elif "Celecon" in self.cpuNameStdout:
                self.cpuBrand += " 赛扬™系列"

        self.resize(500, 100)
        self.setWindowTitle("CPU Information")
        self.cpuNameLabel = QLabel("CPU型号:", self)
        self.cpuCoreLabel = QLabel("CPU核心:", self)
        self.cpuThreadLabel = QLabel("CPU线程:", self)
        self.cpuGhzLabel = QLabel("CPU主频:", self)
        self.cpuBrandLabel = QLabel("CPU品牌:", self)
        if self.showOther:
            self.cpuTypeLabel = QLabel("CPU类型:", self)
            self.mayPlatFormLabel = QLabel("平台(猜测):", self)
        self.cpuNameLine = QLineEdit(self)
        self.cpuCoreLine = QLineEdit(self)
        self.cpuThreadLine = QLineEdit(self)
        self.cpuGhzLine = QLineEdit(self)
        self.cpuBrandLine = QLineEdit(self)
        if self.showOther:
            self.cpuTypeLine = QLineEdit(self)
            self.mayPlatFormLine = QLineEdit(self)

        self.cpuName_h_layout = QHBoxLayout()
        self.cpuCore_h_layout = QHBoxLayout()
        self.cpuThread_h_layout = QHBoxLayout()
        self.cpuGhz_h_layout = QHBoxLayout()
        self.cpuBrand_h_layout = QHBoxLayout()
        self.all_v_layout = QVBoxLayout()
        if self.showOther:
            self.cpuType_h_layout = QHBoxLayout()
            self.mayPlatForm_h_layout = QHBoxLayout()

        self.cpuName_h_layout.addWidget(self.cpuNameLabel)
        self.cpuName_h_layout.addWidget(self.cpuNameLine)
        self.cpuCore_h_layout.addWidget(self.cpuCoreLabel)
        self.cpuCore_h_layout.addWidget(self.cpuCoreLine)
        self.cpuThread_h_layout.addWidget(self.cpuThreadLabel)
        self.cpuThread_h_layout.addWidget(self.cpuThreadLine)
        self.cpuGhz_h_layout.addWidget(self.cpuGhzLabel)
        self.cpuGhz_h_layout.addWidget(self.cpuGhzLine)
        self.cpuBrand_h_layout.addWidget(self.cpuBrandLabel)
        self.cpuBrand_h_layout.addWidget(self.cpuBrandLine)
        if self.showOther:
            self.cpuType_h_layout.addWidget(self.cpuTypeLabel)
            self.cpuType_h_layout.addWidget(self.cpuTypeLine)
            self.mayPlatForm_h_layout.addWidget(self.mayPlatFormLabel)
            self.mayPlatForm_h_layout.addWidget(self.mayPlatFormLine)
        self.all_v_layout.addLayout(self.cpuName_h_layout)
        self.all_v_layout.addLayout(self.cpuCore_h_layout)
        self.all_v_layout.addLayout(self.cpuThread_h_layout)
        self.all_v_layout.addLayout(self.cpuGhz_h_layout)
        self.all_v_layout.addLayout(self.cpuBrand_h_layout)
        if self.showOther:
            self.all_v_layout.addLayout(self.cpuType_h_layout)
            self.all_v_layout.addLayout(self.mayPlatForm_h_layout)

        self.setLayout(self.all_v_layout)

        self.lineInit()

    def lineInit(self):
        self.cpuNameLine.setReadOnly(True)
        self.cpuCoreLine.setReadOnly(True)
        self.cpuThreadLine.setReadOnly(True)
        self.cpuGhzLine.setReadOnly(True)
        self.cpuBrandLine.setReadOnly(True)
        self.cpuNameLine.setText(self.cpuNameStdout)
        self.cpuCoreLine.setText(self.cpuCoreStdout)
        self.cpuThreadLine.setText(self.cpuThreadStdout)
        self.cpuGhzLine.setText(self.cpuGhz)
        self.cpuBrandLine.setText(self.cpuBrand)
        if self.showOther:
            self.cpuTypeLine.setReadOnly(True)
            self.mayPlatFormLine.setReadOnly(True)
            self.cpuTypeLine.setText(self.cpuType)
            self.mayPlatFormLine.setText(self.mayPlatForm)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    MainF = MainForm()
    MainF.show()
    sys.exit(app.exec_())
