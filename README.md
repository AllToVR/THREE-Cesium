# THREE-Cesium
Interactive cesiumJS and THREEjs

This project started with Cesium-threejs-experiment by Wilson Mukar. Please read the original posts here: https://cesium.com/blog/2017/10/23/integrating-cesium-with-threejs/

Abstract: Create a interactive 4D Transactional (could be inventory) Reporting System based upon location, time and data. Utilize CesiumJS to show location and handle time. Utilize THREEjs to display details of your data. I use it to summarize my data the over the entire time period. Requirement of “Interactive”: Clicking an item in one system will make changes in the other system.
 
Location: We are dealing with every legal address worldwide; so: Countries are the category, States are the subcategories and Zip codes are the vsubCategories.

A primary goal of this project was to have EVERYTHING loadable from a “local” CZML file. How you build your file is up to you.
First order of business was to have cesium and threejs data in the same CZML file (3ZML). This required me to parse the file myself. I pull out the cesium data packets and separate them by category, subcategory and vsubcategory, transaction and then everything else. Each one has its own czmlDataSource. There maybe 100+ 3ZML files to load….. All THREEjs data packets create the THREEjs scene on the fly…

Another challenge was real-time rendering. With so many 3ZML files; the system is always building the scene and never returns to the renderer. So I build a timer to delay making the next 3ZML file long enough to allow the renders to do their job. One day I will find a better way…

Picking: The key to making CesiumJS and THREEjs interactive is knowing the ID of the other system. Both systems use a 6 part ID separated by a “-“; “system-subType-category-subcategory-vsubcategory-transaction”. System is “cml” or “three” (I am also interactive with AltSpaceVR). SubType is “Lbl”,”cat”,”sub”,”vsub” and ”trans”. When you choose an entity in CesiumJS; I simply reposition the THREEjs camera in front of that THREEjs object. When you click a THREEjs object; I have CesiumJS FlyTo the location. Zip codes and states FlyTo a different Altitude. Transactions have an extra line to show the infobox. In the THREEjs scene; the plane on the graph representing that transaction is highlighted.

Layout Manager: The order in which information is received cannot be guaranteed; Placing the information into the THREEjs scene needed to be coordinated. Specifically; the layout of category, subcategory and vsubCategory. Also having the layout based upon a users preference is a good thing, but not fully implemented. One user may want to see things front to back, left to right and then top to bottom while another user want things a different way.

Performance side note: I found that if the rendering loop starts before the cesium viewer is fully loaded, the cesium viewer can take 30 seconds to load. So I have the starting of the rendering loop delayed by 3 seconds.

The data files: In the testData directory are all the 3ZML files for this demonstration. There is a file for each country, state and zipcode. Click on “Load Local Files” button. You can load all of them or just select the ones you want to display.

Installation:
BingKey			You will need to get your own Bing key…
Location of script files		This will be the location of the files on your server. Don’t forget the font loading around line 657.

Here are the basic operating instructions of the HTML screen:
Click on “Load Local Files” button. You can load all of them or just select the ones you want to display.
Globe:
Bottom right of globe is the “Full Screen” button. This system is best viewed in this mode!
Click on the ? for instruction on mouse controls
Transactions will appear on the globe (blue balloon) based upon the date and time.
Clicking on a label will zoom to that chart.
Clicking on a transaction (blue balloon) will zoom to that chart and highlight the transaction details.
Clicking on the little camera in the top left corner of the transaction details box; will zoom to the address.

The Chart Area:
Clicking on a chart will zoom the globe.
Clicking on a transaction (small box) will zoom the globe and display the transaction details.
Controls:
Left click + drag = rotate
Right click + drag = left, right, up, down
Scroll wheel = zoom in/out

Conclusion:
This project will drastically improve the quality of “Data Presentation” by bringing together the best of both 3D worlds used in today’s technology.
I look forward to the day when all of this functionality is incorporated into CesiumJS and THREEjs masters.
Mr. Rue LaRue

