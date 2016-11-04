#!/bin/python
#coding=utf-8

import re
from Tkinter import *
from FileDialog import *
import tkMessageBox
from tkFileDialog import askopenfilename

class GooseAndSV_Extract(object):
	"""docstring for ClassName"""
	def __init__(self):
		#创建一个窗口并定义窗口属性
		self.root = Tk()
		self.root.title('小工具')
		self.root.geometry('500x400')

		#定义两个name动态控制label的名称
		self.name1=StringVar()
		self.name2=StringVar()

		#在窗口中添加控件
		self.text=Text(self.root,width=28)
		self.frm=Frame(self.root)
		self.frm1=Frame(self.root)
		self.label1=Label(self.frm1,textvariable=self.name1,font=('Arial',15),fg='blue')
		self.label2=Label(self.frm1,textvariable=self.name2,font=('Arial',15),fg='blue')
		self.button_openGooseFile=Button(self.frm,text='openGooseFile',width=10,command=self.openGooseFile)
		self.button_openSVFile=Button(self.frm,text='openSVFile',width=10,command=self.openSVFile)


	def getContent(self,txt):
		if txt:
			fo=open(txt,'r+')
			content=fo.read()
			return content
		return None

	def getGSTotal(self,txt):	
		#获得txt 文档中的内容
		content=self.getContent(txt)
		if not content:
			print 'txt 文档无效！'
			return None

		#正则匹配出要提取的内容
		pattern=re.compile('\\[GOOSE IN.*?GoCBNum.*?=(.*?)\n',re.S)
		GoCBNum=re.findall(pattern,content)
		return GoCBNum

	def getSVTotal(self,txt):
        #获得txt 文档中的内容
		content=self.getContent(txt)
		if not content:
			print 'txt 文档无效！'
			return None

		#正则匹配出要提取的内容
		pattern=re.compile('\\[SV IN.*?SVNum.*?=(.*?)\n',re.S)
		GoCBNum=re.findall(pattern,content)
		return GoCBNum

	def getGooseModels(self,txt):
		#获得txt 文档中的内容
		content=self.getContent(txt)
		if not content:
			return None

		#正则匹配出要提取的内容
		pattern=re.compile('\\[GoCB\d+\\/\d+\\].*?ref.*?=(.*?)\nAppID',re.S)
		items=re.findall(pattern,content)
		goose=[]
		for item in items:
			goose.append(item)
		return goose

	def getSVModels(self,txt):
        #获得txt 文档中的内容
		content=self.getContent(txt)
		if not content:
			return None

		#正则匹配出要提取的内容
		pattern=re.compile('\\[SVCB\d+\\/\d+\\].*?bySVID.*?=(.*?)\nbyMac',re.S)
		items=re.findall(pattern,content)
		sv=[]
		for item in items:
			sv.append(item)
		return sv

    #设置一个窗口，用于打开txt文档
	def openFile(self):
		filename=askopenfilename(filetypes=(('txt files','*.txt'),('All files','*.*')))
		return filename

	def openGooseFile(self):
		#获取打开文件的路径
		filename=self.openFile()

		#先判断txt文档中goose锻炼个数，如果＝0，则不进去程序
		if self.getGSTotal(filename)==None:
			tkMessageBox.showinfo(title='错误提示',message='您没有打开有效的txt文档，请选择正确的文档！')
			return None
		else:
			if int(self.getGSTotal(filename)==[]):
				tkMessageBox.showinfo(title='错误提示',message='您没有打开有效的txt文档，请选择正确的文档！')
				return None

		if int(self.getGSTotal(filename)[0])==0:
			tkMessageBox.showinfo(title='特别提醒',message='您打开的文档中有0个断链！')
			return None

		#定义一个label的text属性
		self.name1.set('GoCBNum ='+self.getGSTotal(filename)[0])

		#定义一个label
		self.label1.textvariable=self.name1

		#每执行一个openFile方法就清空一次text内容
		self.text.delete('0.0','end')

		#获取goose列表
		gooseLists=self.getGooseModels(filename)

		#定一个count，统计gooseLists的个数,并插入text空间中
		count=0
		for gooseList in gooseLists:
			self.text.insert(1.0,gooseList.lstrip())
			count+=1

		#定义另一个label的text属性
		self.name2.set('Results ='+str(count))

		#定义另一个label
		self.label2.textvariable=self.name2

	def openSVFile(self):
        #获取打开文件的路径
		filename=self.openFile()

		#先判断txt文档中goose锻炼个数，如果＝0，则不进去程序
		if self.getSVTotal(filename)==None:
			tkMessageBox.showinfo(title='错误提示',message='您没有打开有效的txt文档，请选择正确的文档！')
			return None
		else:
			if int(self.getSVTotal(filename)==[]):
				tkMessageBox.showinfo(title='错误提示',message='您没有打开有效的txt文档，请选择正确的文档！')
				return None

		if int(self.getSVTotal(filename)[0])==0:
			tkMessageBox.showinfo(title='特别提醒',message='您打开的文档中有0个断链！')
			return None

		#定义一个label的text属性
		self.name1.set('SVNum ='+self.getSVTotal(filename)[0])

		#定义一个label
		self.label1.textvariable=self.name1

		#每执行一个openFile方法就清空一次text内容
		self.text.delete('0.0','end')

		#获取goose列表
		svLists=self.getSVModels(filename)

		#定一个count，统计gooseLists的个数,并插入text空间中
		count=0
		for svList in svLists:
			self.text.insert(1.0,svList.lstrip())
			count+=1

		#定义另一个label的text属性
		self.name2.set('Results ='+str(count))

		#定义另一个label
		self.label2.textvariable=self.name2

	def start(self):
		self.frm.pack()
		self.frm1.pack()
		self.button_openGooseFile.pack(side=LEFT)
		self.button_openSVFile.pack(side=RIGHT)
		self.label1.pack(side=LEFT)
		self.label2.pack(side=RIGHT)
		self.text.pack()

		self.root.mainloop()

if __name__=='__main__':
	gooseAndSV_Extract=GooseAndSV_Extract()
	gooseAndSV_Extract.start()

		
		

