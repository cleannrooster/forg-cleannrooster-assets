## Animation Interchangeability

All humanoid mobs in this repository are built against a shared skeleton
specification — identical bone names, hierarchy, and pivot points across every
rig. This means every animation in the repository is compatible with every
humanoid mob, without modification.

---

### What this means in practice

Any animation file made for a humanoid entity — embedded in a `.bbmodel' file — can be applied to any
humanoid mob in the repository and will function correctly. You are not
limited to the animations that ship with a specific mob.

This also extends to armor sets converted from humanoid mobs following the
conversion guide. A converted armor set inherits the same skeleton
specification and will accept any animation from the shared pool without
additional rigging work.

---

### The shared skeleton specification

All humanoid rigs are built to the following bone structure. Any animation
authored against this structure is interchangeable across the full set.

---

### Authoring new animations

If you author new animations for any humanoid mob in this repository, those
animations will work on every other humanoid mob without modification,
provided the bone names and hierarchy above are respected. This makes the
system fully extensible — any animation added to the pool is immediately
available across the entire character set.