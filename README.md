# Exporting-Google-Drive-Folder-Image-File-Source-URLs

## Input
![image1](https://user-images.githubusercontent.com/87423131/209308858-81e1a576-3f40-4c53-b09a-7d10fa716800.png)

![image2](https://user-images.githubusercontent.com/87423131/209309032-464253ce-6f6d-47f2-9d05-320bbd7e69cc.png)

## Output
![Google Sheets Results](https://user-images.githubusercontent.com/87423131/209308401-4b5ab9df-6a71-4921-b0ad-bc74db7392fe.png)

**[ Drive Link ](https://drive.google.com/drive/folders/1FsXYBODKPusOmJdSwLwgY90srwNivsW7) | [ Google Sheets Link ](https://docs.google.com/spreadsheets/d/1jAyNfhcRlMZaEC0wOCgclRcJm-nfSNT5pZSo9CfgfG4/edit?usp=sharing)**

# Google Apps Script
```
// https://drive.google.com/uc?id=1TZy8ENDqSOnblJxAMszQTYCE_Dvb6Bwz&export=download

let data = [];

const getData = () => {
  const folderId = "1FsXYBODKPusOmJdSwLwgY90srwNivsW7";
  const ss = SpreadsheetApp.openById("1jAyNfhcRlMZaEC0wOCgclRcJm-nfSNT5pZSo9CfgfG4");
  const sheet = ss.getSheetByName("Sheet1");

  const workingFolder = DriveApp.getFolderById(folderId);

  const folders = workingFolder.getFolders();

  while(folders.hasNext()){
    const folder = folders.next();
    const folderName = folder.getName();

    const files = folder.getFiles();
    
    while(files.hasNext()){
      const file = files.next();
      const fileName = file.getName();
      const fileId = file.getId();
      data.push([folderName, fileName, `https://drive.google.com/uc?id=${fileId}&export=view`])
    }
  }

  sheet.getRange(2, 1, data.length, 3).setValues(data)
}


// this code is for when folder's have no child folders

```
