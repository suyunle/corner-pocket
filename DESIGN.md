---
version: alpha
name: Corner Pocket
description: A Korean carom hall with blue cloth, walnut furniture, brass details and warm practical lighting.
colors:
  background: "#100c0a"
  foreground: "#f1e8d8"
  brass: "#d6b062"
  scoreboardTimber: "#6b3b22"
  scoreboardLamp: "#ffd9a0"
  scoreboardWhite: "#f3efe4"
  scoreboardYellow: "#f2c428"
  scoreboardOrange: "#ec7420"
typography:
  display:
    fontFamily: "Black Han Sans, Malgun Gothic, system-ui, sans-serif"
  body:
    fontFamily: "IBM Plex Sans KR, Malgun Gothic, system-ui, sans-serif"
omitted:
  - section: spacing
    reason: "The changed object is modelled in metres; existing page spacing stays owned by index.html."
  - section: rounded
    reason: "Physical geometry uses bevels; no global CSS radius is introduced."
  - section: components
    reason: "The changed surface is the existing Three.js scoreboard, described below."
---

# Corner Pocket design context

## Overview

A playable Korean billiard hall. Preserve the existing timber-panelled room, blue table cloth, subdued background and Korean game controls. The user's reference for the scoreboard is a freestanding wooden club abacus with horizontal wires, alternating red and ivory beads, and a narrow left compartment. The final requested layout has three wires. The signature is warm light on credible furniture construction.

## Colors

Runtime ownership remains in `index.html`: CSS `:root` owns the existing interface palette and typography. The scoreboard clones the hall's `woodMat`, `darkWoodMat` and `brassMat`, including the shared `woodTex`, with a more matte finish. Do not introduce a separate pale grain texture or a bright orange timber palette. `BALL_HEX` is the shared source for the balls, scoreboard beads and player markers. The values above mirror those owners. Beads use two colours only, white and orange (#ec7420), alternating in fives; the first wire starts white, the second orange and the third white again, with restrained resin highlights. Each player's wire counts down: the points to make are pulled forward at the start (a target of 10 pulls 10; the 4구 쿠션 finish has no bead of its own) and one goes back per point.

## Typography

Keep the existing Black Han Sans display and IBM Plex Sans KR body families, with Korean system fallbacks. The scoreboard has no lettering. Do not add unrelated signage or promotional copy.

## Layout

The existing full-screen scene and responsive control dock stay canonical. `SB_POS` places the scoreboard along the far wall with 8 cm clearance behind its feet; `SB_SIZE` owns its 1.16 m width and 0.76 m foot depth and feeds avatar collision bounds. Two `SB_SOFAS` flank it with 32 cm cabinet-to-arm gaps. They reuse the existing burgundy sofa builder and materials, with 1.12 m seats rather than the side-wall sofas' 1.6 m seats; height, depth, arms and plinth remain identical. Both sofas face the room and have walking collision bounds. The cabinet has exactly three wires: white player, yellow player, and an unscored spare. Each active wire shows points remaining: the opening target is pulled left and each earned point moves one bead back right. Bead capacity grows from 40 to the selected target (up to 99), with thickness and spacing adjusted to prevent overlap.

## Elevation & Depth

Use a recessed back panel, projecting cap and sill, aged brass fasteners and restrained floor contact shading. The user's room-matching refinement calls for the same dark furniture finishes as the tables and no visible glowing strip or dedicated floor light. The scoreboard's top rail is plain timber: no lettering or maker's plate. A concealed wash uses the sconces' warm color at intensity 0.42; wood clearcoat is 0.12 and bead clearcoat is 0.3. Retain the ball hues without bright reflective hotspots. The cabinet is supported by continuous 9.5 cm posts, broad sled feet, rubber pads, a low cross stretcher and front/rear knee braces. Timber joints must meet visibly.

## Shapes

Use softened wooden edges and lenticular beads with narrow collars. Avoid thin stick legs, flat disc placeholders, floating panels and neon outlines.

## Components

`SB.update()` derives remaining beads as `clamp(target - scores[player], 0, target)` from the existing earned-score state. A 4-ball foul restores one bead, never above the opening target; 10-point play therefore starts at 10, drops to 9 on a point, and returns to 10 on a foul. Existing 3-cushion misses and 4-ball finishing-cushion rules remain unchanged. New racks, target changes and newly joined players start with beads already placed; ordinary points and fouls animate in `SB.tick()`. The first two rows belong to white and yellow respectively; left markers identify them. The spare has no player marker and stays unscored. Reuse the existing state pipeline. Instanced bead meshes use six batches across three wires. Honour reduced motion by placing beads immediately. Lights do not allocate additional shadow maps.

## Do's and Don'ts

Keep amber warmth localized to the cabinet and its immediate floor area. Preserve readability and the hall's darker atmosphere. Verify capacity changes at targets 40/41 and 99, score resets, rendering at desktop and phone widths, and the enlarged furniture collision footprint. Do not change game rules or unrelated controls for a furniture redesign.
