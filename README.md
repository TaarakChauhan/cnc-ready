# CNC Ready

A 3D machine-shop tycoon in one HTML file. You carry stock, run the mills, serve the client, and spend the cash until the garage becomes a plant.

**Play it:** https://cnc-ready-mystof-realm-s-projects.vercel.app

The whole game is [`index.html`](index.html). Open that file in a desktop browser, or use the link above. The page loads Three.js r160 from cdnjs, so the first load needs a network connection.

## How to play

1. Press **Start the shift**.
2. Pick up aluminum stock at the raw rack.
3. Stand on the mill **input** pad. The stock drops in and the spindle runs.
4. Pick up the finished bracket on the **output** pad.
5. Deliver it to the order counter. The client pays when the order is complete.
6. Stand on the cash pad to pocket the bills.
7. Stand on a glowing pad to buy the next upgrade. Cash drains while you stand there, and a partial payment is kept if you walk off.

The first client always orders one aluminum bracket. Later clients ask for bigger jobs.

## Controls

| Input | Action |
| --- | --- |
| Mouse or trackpad click | Walk to that spot on the floor. A yellow ring marks the destination. |
| Mouse or trackpad drag | Steer while the button is held. Release to stop. |
| Tap a machine | Change that machine's job. |
| WASD or arrow keys | Walk. Camera-relative: W moves away from the camera. |
| Phone joystick | Walk. Shown on touch screens. |
| U | Open the upgrades sheet. |
| Esc | Close the sheet. |

Keys and the joystick cancel a click-to-walk order. Buttons, the upgrades sheet, and the start card do not move the character.

## What you are building

You start in the garage with $5, one mill, a stock rack, and an order counter. Carry capacity starts at 4. Money is whole dollars.

Zones open in order: **Garage**, **Workshop Wing**, **Factory Floor**, **Industrial Plant**.

| Unlock | Cost | What it adds |
| --- | ---: | --- |
| Work Boots | $12 | Faster movement |
| Carry Vest | $30 | Two more carry slots |
| Manual Saw | $45 | Cut stock so later cycles are shorter |
| CNC Lathe | $90 | Shafts, flanges, and gear finishing |
| Hire Operator | $150 | Loads raw stock into machines |
| Workshop Wing | $260 | Opens the west wing |
| Deburr Station | $400 | Finished parts sell for more |
| Hire Hauler | $380 | Carries finished parts |
| Gear Program | $650 | Mill a blank, then finish it on the lathe |
| Inspection | $720 | A passed check adds a tip |
| Hire Cashier | $900 | Serves the counter and collects cash |
| Housing Fixture | $1,200 | The mill can cut engine housings |
| Factory Floor | $1,800 | Opens the north bay |
| Packing Station | $2,200 | Boxes three matching parts into a crate |
| Second Mill | $2,600 | Another spindle |
| 5-Axis Cell | $3,000 | Slow, high-value impellers |
| Industrial Plant | $4,500 | Opens the east plant |
| Loading Dock | $5,200 | Trucks buy crates |
| AGV Forklift | $6,000 | Hauls crates onto the truck |
| Front Office | $8,000 | The shop earns passive income |

The shop sheet sells speed, carry, spindle, output, price, client flow, and crew upgrades. After the office is open, it also hires up to three managers.

**Open a new factory** is the prestige reset. It is available after $10,000 lifetime earnings or after the office is built. Machines, cash, and shop upgrades reset. Pay is permanently multiplied by 0.25 each time, starting from x1.00.

## Parts

| Part | Base price | Where it is made |
| --- | ---: | --- |
| Aluminum Bracket | $8 | Mill |
| Steel Shaft | $18 | Lathe |
| Flange | $26 | Lathe |
| Gear | $42 | Mill makes a blank, lathe finishes it |
| Engine Housing | $74 | Mill, after the housing fixture |
| Turbine Impeller | $160 | 5-axis cell |

A crate is three of the same part and pays a bonus. Deburr and inspection raise the sale price. Sell price also grows with the price upgrade and with prestige.

## Crew

| Role | Job |
| --- | --- |
| Operator | Brings stock to a machine that needs it |
| Hauler | Carries finished parts toward the counter |
| Cashier | Serves the counter and picks up cash |
| Forklift | Moves crates to the truck |
| Manager | Raises office income. Hired from the sheet, up to 3 |

Workers walk around obstacles. They do not teleport.

## Saving

Progress is stored in this browser under the key `cnc-ready-v1`.

Saved: cash, unlocks, partial pad payments, crew, upgrade levels, prestige, and the sound setting.

Not saved: parts in your hands, parts in the air, and clients already in line.

The game writes the save about every 2 seconds during a shift, when you continue, and when the tab closes. **Upgrades → Reset** clears that save and reloads. A new visit with no save shows **Start the shift**. A saved visit shows **Continue the shift**.

`index.html?test=1` runs the built-in playtest and does not read or write the save. The page title becomes `TEST_OK` or `TEST_FAIL`.

## Project layout

There is no build step and no package manager.

| File | Purpose |
| --- | --- |
| `index.html` | The game: page, styles, and simulation |
| `README.md` | This page |

Balance numbers live in the `CONFIG` object at the top of the script: prices, cycle times, unlock costs, camera, and speeds. Textures are drawn in code from a fixed seed, so the shop looks the same on every load.

Rendering uses Three.js r160 (`three.min.js` from cdnjs), MeshStandard materials, and a soft shadow map. People and machines are solid shapes on purpose so the shop stays readable from the isometric camera.

## Deploy

The live site is a Vercel project named `cnc-ready` on the MystofRealm team. Production:

https://cnc-ready-mystof-realm-s-projects.vercel.app

Pushing `main` deploys that site when the GitHub repository is connected to the Vercel project. The site is a static `index.html`. No install or build command is required.
