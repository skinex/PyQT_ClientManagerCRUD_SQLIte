# PyQY DBManager
This is a small desktop app built on PyQT framework and using SQLIte as DB 
The user interface is created in QtDesigner. The implementation used PyQT5 framework version.
====================
Database connection code:
```python
self.db = QtSql.QSqlDatabase.addDatabase('QSQLITE')
self.db.setDatabaseName('fieldlist.db')
```
Code for querying row and presenting it in tableView:
```python
self.model = QtSql.QSqlTableModel()
self.model.setTable('field')
self.model.setEditStrategy(QtSql.QSqlTableModel.OnFieldChange)
self.model.select()
self.model.setHeaderData(0, QtCore.Qt.Horizontal,"id")
self.model.setHeaderData(1, QtCore.Qt.Horizontal,"Name")
self.model.setHeaderData(2, QtCore.Qt.Horizontal, "Surname")
self.model.setHeaderData(3, QtCore.Qt.Horizontal, "DOB")
self.model.setHeaderData(4, QtCore.Qt.Horizontal,"Phone")
self.ui.tableWidget.setModel(self.model)
```
Code for row insertion:
```python
self.model.insertRows(self.i,1)
self.model.setData(self.model.index(self.i,1),self.ui.lineEdit.text())
self.model.setData(self.model.index(self.i, 2), self.ui.lineEdit_2.text())
self.model.setData(self.model.index(self.i,4), self.ui.lineEdit_3.text())
self.model.setData(self.model.index(self.i,3), self.ui.dateEdit.text())
self.model.submitAll()
```
Code for update row:
```python
if self.ui.tableWidget.currentIndex().row() > -1:
     record = self.model.record(self.ui.tableWidget.currentIndex().row())
     record.setValue("Name",self.ui.lineEdit.text())
     record.setValue("Surname",self.ui.lineEdit_2.text())
     record.setValue("DOB", self.ui.dateEdit.text())
     record.setValue("Phone", self.ui.lineEdit_3.text())
     self.model.setRecord(self.ui.tableWidget.currentIndex().row(), record)
else:
     QMessageBox.question(self,'Message', "Please select a row would you like to update", QMessageBox.Ok)
     self.show()
```
Code for deletingr row:
```python
if self.ui.tableWidget.currentIndex().row() > -1:
    self.model.removeRow(self.ui.tableWidget.currentIndex().row())
    self.i -= 1
    self.model.select()
    self.ui.lcdNumber.display(self.i)
else:
    QMessageBox.question(self,'Message', "Please select a row would you like to delete", QMessageBox.Ok)
    self.show()
```
![alt text](https://github.com/skinex/CRUD-SQLite-/blob/master/project.png)
