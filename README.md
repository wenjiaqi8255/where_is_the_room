<aside>
💡 English version is below
</aside>

also see this in my website: https://wenjiaqi.notion.site/10-30-Mark-30-student-dormitories-in-Munich-on-Google-Maps-in-10-minutes-53c4586995f44b40b0961bdb5638958e?pvs=4


# A. 爬数据并借用谷歌地图可视化 / Scrape data and visualize using Google Maps

# 0. 介绍 / Introduction

在慕尼黑租房是一个非常困难的过程。尽管学生会（Studierendenwerk）提供了一些私人住房选择，但这些信息没有地图显示，给外地学生尤其是对慕尼黑不熟悉的学生带来了极大的不便。因此，我希望通过可视化手段展示这些住房的位置，以便更好地了解和选择适合自己的居住地点。

Finding rental housing in Munich is a challenging process. Although the Studierendenwerk provides some private housing options, these listings lack a map, which poses significant difficulties, especially for students unfamiliar with Munich. Therefore, I aim to use visualization techniques to display the locations of these housing options, making it easier to understand and choose suitable living arrangements.

# 1. 过程

#English Version is below

## 0.拿到数据（可选）

我：我怎么把网页上的信息保存成表格的形式？

> ChatGPT:
> 
> 
> 要将网页上的信息保存成表格的形式，您可以按照以下步骤操作：
> 
> 1. **使用浏览器扩展程序**：
>     - 您可以使用浏览器扩展程序，如“Table Capture”或“Scraper”，来抓取网页上的表格数据。
>     - 这些扩展程序通常可以将抓取到的数据直接导出为CSV或Excel文件。
> 2. **使用编程语言（例如Python）**：
>     - 您可以使用Python的`requests`库来获取网页的HTML内容，然后使用`BeautifulSoup`库来解析HTML并提取表格数据。
>     - 提取的数据可以使用`pandas`库保存为CSV或Excel文件。
>     
>     下面是一个简单的示例代码，展示如何使用Python提取网页表格数据并保存为CSV文件：
>     
>     ```jsx
>     import requests
>     from bs4 import BeautifulSoup
>     import pandas as pd
>     
>     # 发送HTTP请求获取网页内容
>     url = '网页URL'
>     response = requests.get(url)
>     soup = BeautifulSoup(response.content, 'html.parser')
>     
>     # 查找网页中的表格
>     table = soup.find('table')
>     
>     # 提取表格中的数据
>     headers = [header.text for header in table.find_all('th')]
>     rows = []
>     for row in table.find_all('tr'):
>         cells = row.find_all('td')
>         if cells:
>             rows.append([cell.text for cell in cells])
>     
>     # 将数据保存为DataFrame
>     df = pd.DataFrame(rows, columns=headers)
>     
>     # 保存为CSV文件
>     df.to_csv('table_data.csv', index=False)
>     
>     ```
>     

## 1. 问ChatGPT

我：我想要在地图上标注我手上的一系列地址，怎么方便地做这件事

> ChatGPT:
> 
> 
> 标注地图上的一系列地址，你可以使用几种方法，具体取决于你的需求和可用工具：
> 
> 1. **Google 地图**：
>     - 使用 Google 地图的“我的地图”功能来创建和保存自定义地图。
>     - 操作方法：访问 Google 地图网站，登录账户后，点击左侧菜单的“我的地方”，选择“地图”标签后点击“创建地图”。
>     - 在新地图页面中，你可以通过搜索框搜索地址并添加到地图上，或者手动标记位置。
>     - 你还可以为每个位置添加详细信息，如名称、描述等。
> 2. **Excel 或 Google 表格与地图应用结合**：
>     - 如果你的地址列表很长，可以首先在 Excel 或 Google 表格中整理这些地址。
>     - 然后，使用 Google 表格的“地理编码”插件将地址转换为经纬度。
>     - 将转换好的经纬度使用上述 Google 地图的“我的地图”功能导入，进行批量标注。
> 3. **ArcGIS 或 QGIS**：
>     - 如果你有GIS（地理信息系统）软件的使用经验，ArcGIS 和 QGIS 是更为专业的选择。
>     - 这些软件支持更复杂的地理数据分析和视觉化展示。
>     - 你可以导入包含地址的表格数据，使用内置的地理编码工具将地址转换为地图上的点。
> 4. **开源或编程解决方案**：
>     - 如果你具备一定的编程技能，可以使用 Python 等编程语言配合地理编码库（如 Geopy）和绘图库（如 Folium 或 Plotly）来实现。
>     - 这种方法可以提供更高的自定义程度和自动化处理大量数据的能力。

## 2. 从地址生成经纬度

我：地理编码这个插件在哪里

> ChatGPT:
> 
> 
> 要在 Google 表格中使用地理编码插件，你需要通过以下步骤来找到并安装它：
> 
> 1. **打开 Google 表格**：
>     - 创建一个新的表格或打开一个已有的表格。
> 2. **访问“扩展程序”菜单**：
>     - 在表格的顶部菜单栏中，找到“扩展程序”选项并点击它。
> 3. **获取扩展程序**：
>     - 在下拉菜单中选择“获取扩展程序”。这将打开 Google 工作区市场。
> 4. **搜索地理编码插件**：
>     - 在市场的搜索框中，输入“地理编码”或者“Geocode”等关键词进行搜索。
>     - 常用的插件例如“Awesome Table”、“Geocode by Awesome Table”或其他地理编码工具。
> 5. **安装插件**：
>     - 找到你需要的插件后，点击它进入详细页面。
>     - 点击“安装”按钮，按照提示完成安装过程。
> 6. **使用插件**：
>     - 安装完成后，回到你的 Google 表格。
>     - 再次打开“扩展程序”菜单，你将看到新安装的插件已列在菜单中。
>     - 点击该插件，按照具体的指示使用地理编码功能。
> 
> 通过这些步骤，你可以将PDF中的地址列表整理到Google表格中，并使用地理编码插件将地址转换为经纬度，进而进行地图标注。如果你在操作过程中遇到任何困难，随时告诉我，我可以提供进一步的帮助！
> 

[ChatGPT](https://chat.openai.com/share/0d2b530d-f0fd-4ce1-9c12-efe1159ceb75)

## 3. 整理数据（可选）

我：它们现在还没有用引号包围，在一个表格里面，我要怎么加上引号

> ChatGPT:
> 
> 
> 如果你的数据当前存储在一个表格中（如Excel或Google表格），并且需要将文本字段用引号包围以准备导出为CSV文件，你可以通过以下步骤在Excel中轻松完成这个任务：
> 
> ### **在Excel中添加引号**
> 
> 1. **创建辅助列**:
>     - 在你的数据旁边，添加一个新列。假设你的名称位于A列，你可以在B列添加引号。
>     - 在B1单元格（或数据起始行的单元格）输入公式：**`="""" & A1 & """"`**。这个公式将A1单元格的内容包围以双引号。
> 2. **拖动填充句柄**:
>     - 将这个公式向下拖动到整列，这样所有的名称都将被双引号包围。
> 3. **对其他需要引号的列重复此步骤**:
>     - 如果评论在C列，你可以在D列使用类似的公式：**`="""" & C1 & """"`**，并向下填充。
> 4. **导出为CSV**:
>     - 当所有需要引号的文本都已处理后，选择文件菜单中的“保存为”，选择保存格式为CSV（逗号分隔）。
> 
> 确保在导出前检查文件，验证所有文本字段都正确地被引号包围，特别是那些包含逗号或引号的字段。这样可以确保当你导入到Google“我的地图”或其他地图服务时，字段不会因格式错误而被错误解析。
> 
> 如果你使用的是Google表格，步骤相似，但是Google表格在保存为CSV时通常会自动处理文本字段的引号。如果你有任何疑问或需要进一步帮助，请告诉我！
> 

## 4. 放进谷歌地图

我：我现在有一系列经纬度了，要怎么把他们都标在地图上

> ChatGPT:
> 
> 
> 既然你已经拥有了一系列经纬度，接下来可以使用 Google 地图的“我的地图”功能来批量地标注这些经纬度。下面是详细的步骤：
> 
> ### **1. 准备数据**
> 
> 确保你的经纬度数据是以可导入的格式存储，通常是 CSV 文件。这个文件应该包含至少两列，一列是经度，另一列是纬度。你可以在 Excel 或 Google 表格中准备这些数据，然后保存为 CSV 文件。
> 
> ### **2. 打开 Google “我的地图”**
> 
> - 访问 [Google 我的地图](https://www.google.com/maps/d/)。
> - 如果你还没有登录，需要先登录你的 Google 账户。
> 
> ### **3. 创建新地图**
> 
> - 点击“创建新地图”按钮。
> - 一个新的地图界面会打开，你可以在左上角给地图命名。
> 
> ### **4. 导入你的数据**
> 
> - 在地图的菜单中，点击“导入”按钮。
> - 选择你的 CSV 文件上传。
> - 根据提示，选择经度和纬度列，以确保 Google 正确地读取这些数据。
> - 上传并处理完毕后，你的所有经纬度将作为标记添加到地图上。
> 
> ### **5. 调整和优化地图**
> 
> - 你可以为每个标记编辑详细信息，如名称、描述或添加照片。
> - 可以更改标记的图标，分类不同类型的位置。
> - 调整图层设置，如果有多个数据集，可以为每个数据集创建一个图层。
> 
> ### **6. 保存和分享地图**
> 
> - 确保你的地图被保存（通常 Google 会自动保存）。
> - 你可以通过点击“分享”按钮，并设置相应的权限，将地图分享给其他人或者嵌入到网站中。
> 
> 使用这种方法，你可以轻松地将大量经纬度数据标注到 Google 地图上，用于分析、展示或共享。如果有任何具体问题或需要进一步的帮助，请随时告诉我！
> 

---

# 1. Process

#English version 

Right-click on 'original' to go to Google Maps

(I don't know why they don’t give a map in the first place, there is just a PDF…)

(Also the title is lying, it took me half an hour)

---

If you're interested, here's the process:

## 0.Get the Data (optional)

Me: Tell me how to get the data from the website with table format

> ChatGPT:
> 
> 
> To save information from a webpage into a table format, you can follow these steps:
> 
> 1. **Using Browser Extensions**:
>     - You can use browser extensions such as "Table Capture" or "Scraper" to scrape table data from the webpage.
>     - These extensions usually allow you to export the scraped data directly as CSV or Excel files.
> 2. **Using a Programming Language (e.g., Python)**:
>     - You can use Python's `requests` library to get the HTML content of the webpage, and then use the `BeautifulSoup` library to parse the HTML and extract the table data.
>     - The extracted data can be saved as a CSV or Excel file using the `pandas` library.
>     
>     Below is a simple example code that demonstrates how to use Python to extract table data from a webpage and save it as a CSV file:
>     
>     ```jsx
>     import requests
>     from bs4 import BeautifulSoup
>     import pandas as pd
>     
>     # 发送HTTP请求获取网页内容
>     url = '网页URL'
>     response = requests.get(url)
>     soup = BeautifulSoup(response.content, 'html.parser')
>     
>     # 查找网页中的表格
>     table = soup.find('table')
>     
>     # 提取表格中的数据
>     headers = [header.text for header in table.find_all('th')]
>     rows = []
>     for row in table.find_all('tr'):
>         cells = row.find_all('td')
>         if cells:
>             rows.append([cell.text for cell in cells])
>     
>     # 将数据保存为DataFrame
>     df = pd.DataFrame(rows, columns=headers)
>     
>     # 保存为CSV文件
>     df.to_csv('table_data.csv', index=False)
>     
>     ```
>     

## 1. Ask ChatGPT

Me: I want to mark a series of addresses on my map. How do I do that easily?

> ChatGPT:
> 
> 
> To mark a series of addresses on a map, you can use several methods, depending on your needs and available tools:
> 
> 1. **Google Maps**:
>     - Use the 'My Maps' feature of Google Maps to create and save custom maps.
>     - How to operate: Visit the Google Maps website, log in to your account, click on 'My Places' in the left menu, select the 'Maps' tab, and click 'Create Map'.
>     - In the new map page, you can search for addresses through the search box and add them to the map, or manually mark locations.
>     - You can also add detailed information for each location, such as name, description, etc.
> 2. **Combining Excel or Google Sheets with Map Applications**:
>     - If you have a long list of addresses, you can first organize these addresses in Excel or Google Sheets.
>     - Then, use the 'Geocode' plugin of Google Sheets to convert addresses into longitude and latitude.
>     - Import the converted longitude and latitude using the 'My Maps' feature of Google Maps mentioned above for batch marking.
> 3. **ArcGIS or QGIS**:
>     - If you have experience using GIS (Geographic Information System) software, ArcGIS and QGIS are more professional choices.
>     - These software support more complex geographic data analysis and visual display.
>     - You can import tabular data that contains addresses and use the built-in geocoding tool to convert the addresses into points on the map.
> 4. **Open-source or Programming Solutions**:
>     - If you have certain programming skills, you can use programming languages like Python to implement this, in combination with geocoding libraries (like Geopy) and plotting libraries (like Folium or Plotly).
>     - This method can provide a higher degree of customization and the ability to automatically process large amounts of data.

## 2. Generate Longitude and Latitude from Addresses

Me: Where is the geocoding plugin?

> ChatGPT:
> 
> 
> To use the geocoding plugin in Google Sheets, you need to find and install it using the following steps:
> 
> 1. **Open Google Sheets**:
>     - Create a new sheet or open an existing sheet.
> 2. **Access the 'Extensions' Menu**:
>     - In the top menu bar of the sheet, find and click on the 'Extensions' option.
> 3. **Get Extensions**:
>     - In the dropdown menu, select 'Get Extensions'. This will open the Google Workspace Marketplace.
> 4. **Search for the Geocoding Plugin**:
>     - In the search box of the marketplace, enter keywords like 'Geocoding' or 'Geocode' to search.
>     - Commonly used plugins include 'Awesome Table', 'Geocode by Awesome Table', or other geocoding tools.
> 5. **Install the Plugin**:
>     - After finding the plugin you need, click on it to go to its details page.
>     - Click the 'Install' button and follow the prompts to complete the installation.
> 6. **Use the Plugin**:
>     - After installation, go back to your Google Sheets.
>     - Open the 'Extensions' menu again, and you will see the newly installed plugin listed in the menu.
>     - Click on the plugin and use the geocoding function according to specific instructions.
> 
> Through these steps, you can organize the address list in the PDF into Google Sheets and use the geocoding plugin to convert the addresses into longitude and latitude, and then mark them on the map. If you encounter any difficulties in the process, let me know at any time, I can provide further help!
> 

[ChatGPT](https://chat.openai.com/share/0d2b530d-f0fd-4ce1-9c12-efe1159ceb75)

## 3. Organize Data (optional)

Me: They are not yet enclosed in quotation marks, they are in a spreadsheet, how do I add quotation marks?

> ChatGPT:
> 
> 
> If your data is currently stored in a spreadsheet (like Excel or Google Sheets), and you need to encase text fields in quotes to prepare for exporting as a CSV file, you can easily accomplish this task in Excel using the following steps:
> 
> ### **Adding Quotations in Excel**
> 
> 1. **Create Auxiliary Column**:
>     - Add a new column next to your data. Assuming your name is in column A, you can add quotes in column B.
>     - Enter the formula in cell B1 (or the cell of the starting row of data): **`="""" & A1 & """"`**. This formula will enclose the content of cell A1 in double quotes.
> 2. **Drag Fill Handle**:
>     - Drag this formula down the entire column, so that all names will be enclosed in double quotes.
> 3. **Repeat this Step for Other Columns Needing Quotes**:
>     - If comments are in column C, you can use a similar formula in column D: **`="""" & C1 & """"`**, and fill down.
> 4. **Export as CSV**:
>     - Once all text that needs quotes has been processed, select 'Save As' from the file menu, and choose to save the format as CSV (comma delimited).
> 
> Be sure to check the file before exporting, verify that all text fields are correctly enclosed in quotes, especially those fields that contain commas or quotes. This ensures that when you import into Google 'My Maps' or other map services, the fields will not be misinterpreted due to formatting errors.
> 
> If you are using Google Sheets, the steps are similar, but Google Sheets usually automatically handles the quotes of text fields when saving as CSV. If you have any questions or need further help, please let me know!
> 

## 4. Put into Google Maps

Me: I now have a series of longitude and latitude coordinates, how do I mark them all on the map?

> ChatGPT:
> 
> 
> Now that you already have a series of longitude and latitude, you can use the 'My Maps' feature of Google Maps to bulk mark these coordinates. Here are the detailed steps:
> 
> ### **1. Prepare Data**
> 
> Make sure your longitude and latitude data is stored in a format that can be imported, usually a CSV file. This file should contain at least two columns, one for longitude and another for latitude. You can prepare these data in Excel or Google Sheets and then save as a CSV file.
> 
> ### **2. Open Google 'My Maps'**
> 
> - Visit [Google My Maps](https://www.google.com/maps/d/).
> - If you are not logged in, you need to log into your Google account first.
> 
> ### **3. Create New Map**
> 
> - Click the 'Create New Map' button.
> - A new map interface will open, and you can name the map in the top left corner.
> 
> ### **4. Import Your Data**
> 
> - In the menu of the map, click the 'Import' button.
> - Choose your CSV file to upload.
> - Follow the prompts to select the columns for longitude and latitude, to ensure that Google correctly reads this data.
> - After upload and processing, all your longitude and latitude will be added to the map as markers.
> 
> ### **5. Adjust and Optimize Map**
> 
> - You can edit detailed information for each marker, such as name, description, or add photos.
> - You can change the icon of the marker, categorize different types of locations.
> - Adjust layer settings, if there are multiple data sets, you can create a layer for each data set.
> 
> ### **6. Save and Share Map**
> 
> - Make sure your map is saved (Google usually saves automatically).
> - You can share your map with others or embed it in a website by clicking the 'Share' button and setting the corresponding permissions.
> 
> Using this method, you can easily mark a large amount of longitude and latitude data on Google Maps for analysis, display, or sharing. If you have any specific questions or need further help, please feel free to tell me!
> 

# 2. 结果 / Outcome
<img width="1508" alt="image" src="https://github.com/wenjiaqi8255/where_is_the_room/assets/127540860/73c68d9f-89be-46b8-9c8e-9e783c392373">

https://www.google.com/maps/d/edit?mid=13hmeqxwm5Kcg2QvXKO-DBgKY-IDv4Kg&usp=sharing

点击⬆️跳转到谷歌地图

# B. 进一步：通勤时间可视化

### 使用Python和Folium进行可视化（可选）

如果您想在本地或通过Web应用程序进行更高级的可视化，您可以使用Python的Folium库。Folium是一个强大的Python库，可以生成基于Leaflet.js的地图。见Jupyter笔记
<img width="542" alt="image" src="https://github.com/wenjiaqi8255/where_is_the_room/assets/127540860/5aa54f3f-434c-4a4e-84cd-78ba006e3d54">

https://wenjiaqi8255.github.io/where_is_the_room/transit_times_map.html

# B. Further: Commute Time Visualization

### Using Python and Folium for visualization 

If you want more advanced visualization locally or through a web application, you can use the Folium library of Python. Folium is a powerful Python library that can generate maps based on Leaflet.js. See Jupyter notes.

https://wenjiaqi8255.github.io/where_is_the_room/transit_times_map.html
