# 🗺️ Sandy Mapdata

## If link gives 404 - use [https://vertex-hub.com/prompt/map-data/sandy-rework](https://vertex-hub.com/prompt/map-data/sandy-rework) and wait 10 minutes



### 🗺️ Understanding and Using MapData for FiveM Maps

When using maps from Prompt's Studio, you may encounter **MapData**, a crucial component that ensures your maps work seamlessly with the interiors downloaded from the Sandy Shores area. This guide will explain what MapData is, how to install it, and how it integrates with your FiveM server.

***

#### 🔍 What is MapData?

Sandy MapData is a configuration resource that ensures compatibility between your GTAV map and the interiors you download for the Sandy Shores area. It acts as a bridge, verifying that the correct interiors are installed and functioning properly with your maps.

If the MapData doesn’t match the installed interiors, your **server console** will notify you with an error and provide a link to download the correct MapData.

_Console message usually appears after all maps have loaded._

***

<details>

<summary>🛠️ How to Use MapData</summary>

**1. Download Interiors from Sandy Area**

* Download the required interiors from Keymaster.
* Install them in your `resources` folder as usual.

**2. Check for MapData at Server Start**

* Upon server start, maps will check for which Sandy interiors are installed.
* If MapData is missing or incorrect, your server console will show an error with a download link.

**3. Install the Correct MapData**

* Download the MapData using the provided link in the console.
* Extract the folder from the `.zip` (do not leave it zipped).
* Place the folder inside your `resources` directory.
* Add this line in your `server.cfg` **after** any maps using it:

```cfg
start cfx_prompt_sandy_mapdata
```

**4. Verify Compatibility**

* The script will compare your installed interiors with MapData’s supported list.
* If they match, the map runs fine.
* If not, it will show another download link in the console.

</details>

***

<details>

<summary>🔧 How MapData Works</summary>

* **Event-Based Verification**: Each Prompt map fires events to check which Sandy interiors are present.
* **Load Order Priority**: MapData must be started **after** any map that uses it.
* **Compatibility Match**: The script compares installed interior resources with those declared inside MapData. If mismatched, a direct GitHub link is shown to fix it.

</details>

***

<details>

<summary>🚨 Troubleshooting</summary>

**❌ Link Doesn’t Work**

If the console link gives a 404 or leads to a missing page, try generating your MapData using the [Prompt MapData Generator](https://vertex-hub.com/prompt/map-data/sandy-rework). Wait 10 minutes after installing a new map before running it. If the issue persists, contact [Prompt Studio on Discord](https://discord.gg/rKbHHdfZFU) and create a ticket with the error message and broken link.

**❌ MapData Mismatch Error**

Make sure:

* You downloaded the correct interiors.
* You installed and extracted the proper MapData version.
* The `cfx_prompt_sandy_mapdata` is **started after** the dependent maps.

</details>

***

#### ✅ Quick Checklist

* [x] Downloaded & installed required interiors
* [x] Checked server console for MapData errors
* [x] Installed MapData and added to `server.cfg`
* [x] Started MapData after maps using it
* [x] Restarted and verified compatibility

***

Enjoy immersive mapping with Prompt's Studio maps — built for realism and server performance. 🚀
