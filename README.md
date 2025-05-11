# rviz_dark_custom_theme






## → 🔧 Dependencies

Make sure you have the following installed:

```bash
sudo apt update
sudo apt install -y ansible        
sudo apt install qt5ct             
```

## → 📝 Configuration Changes

Before you run, update your Qt5ct and Ansible files:

1. **In `main.yml` (lines 32–33):**
    
    ```bash
      qt5ct_conf_file: "/workspace/rviz_dark_custom_theme/qt5ct.conf"
      me_qss_file:     "/workspace/rviz_dark_custom_theme/rviz.qss"
    ```

## 💡 Replacing Default RViz Icons

Changing a tool button’s icon for *all* states purely in QSS can be tricky. A more direct approach is to swap out RViz’s built-in icon files:

```bash
sudo find /opt/ros/humble/share/rviz_default_plugins/icons/classes/ -type f
```

Copy your custom SVG into place (use the exact same filename). This is an example inside the `icons` folder: 
```bash
cp map_point.svg /opt/ros/humble/share/rviz_default_plugins/icons/classes/PublishPoint.svg
cp robot.png /opt/ros/humble/share/rviz_default_plugins/icons/classes/SetInitialPose.png
cp 2dgoal.png /opt/ros/humble/share/rviz_default_plugins/icons/classes/SetGoal.png
```

## → ⚙️ Compile & Install

Run the Ansible playbook to (re)install and configure the theme:

```bash
ansible-playbook -i localhost, main.yml
```


## → ▶️ Run RViz2 with the Dark Theme

1. Set the Qt5ct platform theme for your session:
    
    ```bash
    export QT_QPA_PLATFORMTHEME=qt5ct
    ```
    
2. Launch RViz2 and enjoy the new look:
    
    ```bash
    rviz2
    ```


## → 🗑️ Remove the Theme

If you want to revert back:

```bash
# Remove the QSS file
rm -f ~/.config/qt5ct/qss/me.qss

# Remove or reset the qt5ct config
rm -f ~/.config/qt5ct/qt5ct.conf

# Unset the environment variable
unset QT_QPA_PLATFORMTHEME
```

## → 🔍 Inspect RViz UI at Runtime

Use GammaRay (or another Qt inspector) to peek under the hood:

```bash
gammaray --inprocess rviz2
```

> 🔑 Important panels live under Objects → VisualizationFrame.
> 

