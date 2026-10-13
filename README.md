# Vision and V2I digital shadows of a signalized intersection — demonstration videos

Demonstration material for the paper

> *Vision and V2I-based Digital Shadows of a Signalized Intersection: A Comparative Fidelity Study*, PE-WASUN 2026.

A **digital shadow** is a one-way, online reconstruction of the mobility state of the intersection inside a simulation runtime (SUMO): information flows from the road to the model and never back. The paper builds two shadows of the same real four-arm signalized intersection, one fed by a traffic camera and one by V2I messages, and scores both under one vehicle-level protocol. This repository only hosts the demonstration videos referenced in the paper's appendix. It contains no data, code or results.

## Videos

Both shadows run at the fixed operating points of the paper (Sec. IV-D). The vision operating point was fixed on the first 180 s of this same camera recording, and the paper evaluates it on the full recording, which contains that segment; it also reports the score outside the segment (Sec. VI). The V2I video shows a channel repetition from the evaluation block, disjoint from the repetitions on which the V2I operating point was fixed (Sec. IV-D).

| Shadow | Configuration | Video |
|---|---|---|
| Vision shadow | Full 282.7 s recording of the traffic camera | https://youtu.be/TIbn344XDdI |
| V2I message shadow | Reporting scenario: 2 msg/s, 50 % packet loss, 1.5 m GPS error, decision buffer 0.2 s, on the channel repetition drawn in the paper's occupancy figure | https://youtu.be/S_yOC06OYTo |

### Layout (both videos, 1920×1080)

| | |
|---|---|
| **Top left — reality.** Vision: the camera recording. V2I: the emitting world, a SUMO replay of the observed traffic with every vehicle equipped, i.e. what the messages describe. | **Top right — the shadow in SUMO.** The runtime the shadow writes into, online, from the input received so far. In the vision video the translucent boxes on the approaches, here and in the 3D view below, are drawn for presentation only: they are polygons marking vehicles the camera sees waiting on an approach, not vehicles of the runtime, which holds a vehicle only once it crosses the stop line (Sec. III-B). |
| **Bottom left — 3D view** of the same runtime. Vision: from the corner the real camera hangs from. V2I: from the south, north up like the SUMO views. | **Bottom right — shadow state.** What the shadow itself knows at each instant: vehicles per approach lane and the origin–destination matrix of completed routes, counted as exits are confirmed. |

Arms are labeled N, S, E, W on every panel.

## What the videos are, and are not

- The occupancy table in the vision video is the raw per-lane count of camera contacts on the image plane, the instrument behind the vision occupancy of the paper (Sec. V-C). The paper scores the agreement of that count with the hand-labeled reference; the raw count shown here is **not** that score. In the V2I video it is the count read from the shadow's runtime.
- The "instantiation lag" printed on the vision video is a per-vehicle drawing lag measured from the shadow's own crossing. It is **not** the representation delay of the paper (Sec. V-D), which is measured against the hand-labeled crossing.
- The traffic lights drawn in the SUMO panels, including the V2I "reality" panel, are a static placeholder program of the network. The paper does not model the site's signal plan (Sec. III-A), and vehicles are placed by position, so a vehicle may be drawn crossing on red.
- The origin–destination matrix builds up from zero as routes complete; it uses no reference data.
- The videos are offline compositions of recorded runs: SUMO screenshots keyed by simulation time, a headless render of the 3D view from the shadow's own state log, and the shadow-state tables from the same log. The shadows themselves ran online, and every drawn state comes from input received up to that instant.
- The V2I "reality" is a simulation replay, not a field capture; the paper states this asymmetry and the reasons for it.
- The fidelity numbers of the paper come from its evaluation protocol, not from these videos.

## Reproducibility

The reproducible package (code, ground truths, run outputs) is reserved for the journal version of this work and is not part of this repository.

## Authors

Pablo Barbecho Bautista, Santiago Israel Delgado Pinos, Anthony Vinicio Dominguez Chacha — Department of Electrical Engineering, Electronics, and Telecommunications, Universidad de Cuenca, Cuenca, Ecuador.
