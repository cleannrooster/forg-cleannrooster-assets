## Converting a Humanoid Mob to a Player Armor Set

All humanoid mobs in this repository are built on standard player proportions.
With minimal rig adjustments, any of them can be deployed as wearable player
armor sets.

---

### What you need

- **Azurelib** (recommended) or **Geckolib** (some incompatibilities)
- The `.bbmodel` file for the mob you want to convert
- Blockbench
- Basic familiarity with armor layer structure in Minecraft

---

### Step 1 — Open the model in Blockbench

Open the `.bbmodel` file. The model is already proportioned to player scale,
so no geometry changes are required unless you want to add or remove detail.

---

### Step 2 — Identify the armor layer groups

Mob models are grouped by body region. The groups you need correspond to the
following armor coverage zones:

- **Head** — helmet slot
- **Body/Chest** — chestplate slot
- **Waist** — waist slot, Azurelib only (attached to chestplate, visible when
  leggings are worn) — optional
- **Right Arm / Left Arm** — attached to chestplate slot
- **Right Leg / Left Leg** — leggings slot
- **Right Foot / Left Foot** — boots slot

Any elements that aren't armor — held weapons, backpacks, loose props — should
be moved to a separate group or removed for the armor version.

---

### Step 3 — Remap bone targets to armor attachment points

Reassign each group to match the armor attachment skeleton. The full bone tree
with origin points is as follows:

bipedHead:           origin: [0, 24, 0]
└── armorHead:       origin: [0, 24, 0]
bipedBody:           origin: [0, 24, 0]
├── armorBody:       origin: [0, 24, 0]
└── armorWaist:      origin: [0, 24, 0]
bipedRightArm:       origin: [5, 22, 0]
└── armorRightArm:   origin: [5, 22, 0]
bipedLeftArm:        origin: [-5, 22, 0]
└── armorLeftArm:    origin: [-5, 22, 0]
bipedLeftLeg:        origin: [-1.9, 12, 0]
├── armorLeftLeg:    origin: [-1.9, 12, 0]
└── armorLeftBoot:   origin: [-1.9, 12, 0]
bipedRightLeg:       origin: [1.9, 12, 0]
├── armorRightLeg:   origin: [1.9, 12, 0]
└── armorRightBoot:  origin: [1.9, 12, 0]

Each armor bone shares its origin with its parent biped bone, meaning armor
geometry rotates around the same pivot point as the player limb it's attached
to. All bones are with the arms down, NOT in a T-pose.

---

### Step 4 — Enlarge the geometry

Many humanoid mobs are designed to look lean, as if their armor is already
part of their body. They also lack the second skin layer that player models
use, which means the geometry sits closer to the body than finished armor
would. To make the armor look natural on a player, you will need to inflate
the individual body parts.

A good starting inflate value is **0.51**. Values above **0.6** will start to
look oversized. For more complex armor pieces, you may need to make additional
manual edits on top of the inflate pass. Use your discretion.

---

### Step 5 — Export and register

Export the model geometry as a `.json` for your mod framework of choice.
Register the armor item using your standard armor material and layer texture
paths. For Azurelib or Geckolib armor pipelines, follow that framework's
registration process using the exported geometry directly.

---

### Notes on specific mobs

- **Legion** — the most conversion-ready mob in the repository. Clean and rust
  texture variants give you two armor states from one model. The backpack
  element should be removed or made optional for armor use.
- **Juggmob** — pauldron geometry extends beyond standard player bounds.
  Functions correctly as armor but may clip in tight spaces.
- **Thiefmob** — the hood works well as a standalone helmet-slot piece if you
  want just the head element without converting the full set.
- **Gemini** — the cage helmet is the standout element and can be isolated as
  a standalone helmet without converting the full set.