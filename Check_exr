import os
from operator import itemgetter
from itertools import *

# Shot format based on the Ramses nomenclature 
# more info : https://ramses.rxlab.guide/

# Set the path to the desired folder where the exr are located
shot = "S2P040"
path = fr"S:\SIC3D\SIC5\Projects\moutons\05-SHOTS\moutons_S_{shot}\moutons_S_{shot}_Render\data"

# Define frame range to check
start_frame = 101
end_frame = 152

# iterate through the renderLayers
for rl in os.listdir(path):
    rl_path = fr"{path}\{rl}"

    # collect missing frames
    missing_frames = []
    if len(os.listdir(rl_path)) > 1:
        exr = os.listdir(rl_path)[0]
        exr = exr.split(".")[0]
        for frame in range(start_frame, end_frame+1):
            exr_name = f"{exr}.{frame}.exr"
            exr_path = fr"{rl_path}\{exr_name}"

            if not os.path.isfile(exr_path):
                missing_frames.append(frame)

        # Group frames for better lisibility
        for k, g in groupby(enumerate(missing_frames), lambda x: x[0]-x[1]):
            missing_frames.append(list(map(itemgetter(1), g)))

        for group in missing_frames:
            missing_frames.append(f"{min(group)}-{max(group)}")
    else:
        missing_frames = "Single frame"

    print(f"Render layer:{rl:20} Missing frames: {missing_frames}")
