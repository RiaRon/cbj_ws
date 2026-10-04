# Third-party reference checkouts

Unmodified upstream clones, kept for reference only. Nothing here is imported
at runtime. Code derived from them lives in
`robot_control/src/openarm_quest_teleop/` and says so in each file header.

| Directory | Upstream | Commit | License |
|---|---|---|---|
| `dora-openarm-vr` | https://github.com/enactic/dora-openarm-vr | `072ce98d9c1d781e4b42626639c48f5c8f2ba8ee` (2026-09-18) | Apache-2.0 (`LICENSE.txt`) |
| `dora-openarm-kinematics` | https://github.com/enactic/dora-openarm-kinematics | `6b9844dd95f5fdc6f3518239da523c6f004bc871` (2026-09-18) | Apache-2.0 (`LICENSE`) |

Both require Python >= 3.11 and dora-rs; `dora-openarm-vr` also needs
numpy >= 2.4, scipy >= 1.17 and pyarrow, and `dora-openarm-kinematics` needs
`openarm-control` (mink, MJCF, 8-value arm + stock gripper arrays). Neither is
installed. The Humble runtime is Python 3.10 with numpy 1.21.

What is reused from `dora-openarm-vr`, and where:

| Upstream file | Reuse | Our file |
|---|---|---|
| `src/dora_openarm_vr/udp_receiver.py` | Derived (changes listed in the header) | `openarm_quest_teleop/udp_receiver.py` |
| `src/dora_openarm_vr/quest_receiver.py` | Packet field names, validity codes, the left-handed to right-handed flip and `_FRAME_ROT`, re-expressed in numpy | `openarm_quest_teleop/packet.py` |
| `src/dora_openarm_vr/smoothing.py` | Verbatim copy, optional, off by default | `openarm_quest_teleop/smoothing.py` |

Not reused: the dora node loop, `FRAME_OFFSET_NECK`, `R_FIX`, the trigger to
gripper mapping, and all of `dora-openarm-kinematics` (the existing
`robot_control.kinematics` chain is used for IK instead).
