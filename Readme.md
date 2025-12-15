# Week 07–08: ROS 2 workspace ja Python pakett

Selle nädala eesmärk on õppida:
- kuidas luua ROS 2 Python pakett käsuga `ros2 pkg create`
- kuidas ehitada workspace’i `colcon`iga
- kuidas käivitada enda node `ros2 run` abil
- kuidas korrastada `package.xml` ja `setup.py` metaandmed (maintainer/description/license)

## Eeldused
- Sul töötab kursuse ROS 2 Humble keskkond (Docker/Devcontainer).
- Igas terminalis on ROS 2 sätitud (nt `source /opt/ros/humble/setup.bash`).

## Ülesanne A: loo uus pakett (kohustuslik)

1) Mine workspace’i `src` kausta:
```bash
cd ~/ros2_ws/src
```

2) Loo uus Python pakett (kasuta **sama nime** nagu siin):
- paketi nimi: `week07_08_my_package`
- node nimi: `my_node`

```bash
ros2 pkg create --build-type ament_python --license Apache-2.0 --node-name my_node week07_08_my_package
```

Pärast seda peab sul tekkima kaust:
```
~/ros2_ws/src/week07_08_my_package
```

## Ülesanne B: ehita pakett (kohustuslik)

1) Mine workspace’i juurkausta:
```bash
cd ~/ros2_ws
```

2) Ehita kõik paketid:
```bash
colcon build
```

3) Ehita ainult sinu pakett:
```bash
colcon build --packages-select week07_08_my_package
```

## Ülesanne C: source ja käivita node (kohustuslik)

1) Source’i workspace:
```bash
source install/local_setup.bash
```

2) Käivita node:
```bash
ros2 run week07_08_my_package my_node
```

## Ülesanne D: korrasta package.xml (hindeline)

Ava fail:
```
~/ros2_ws/src/week07_08_my_package/package.xml
```

Tee parandused:
- `description` ei tohi olla `TODO`
- `maintainer` ja `maintainer_email` peavad olema sinu omad
- `license` peab olema `Apache-2.0` või `Apache License 2.0` (vali üks ja kasuta järjekindlalt)

Näidis (oluline on sisu, mitte täpselt sama tekst):
```xml
<description>ROS 2 algõppe harjutuspakett (Week 07–08)</description>
<maintainer email="eesnimi.perenimi@example.com">Eesnimi Perenimi</maintainer>
<license>Apache-2.0</license>
```

## Ülesanne E: korrasta setup.py (hindeline)

Ava fail:
```
~/ros2_ws/src/week07_08_my_package/setup.py
```

Veendu, et järgmised väljad **klapivad package.xml-iga**:
- `maintainer`
- `maintainer_email`
- `description`
- `license`
- `package_name` peab olema `week07_08_my_package` (kui sul tekkis see automaatselt)

Kui vaja, uuenda ka `entry_points` rida, et `my_node` jääks käivitatavaks.

## Esitamine (kohustuslik)
Sinu GitHub repo peab sisaldama:
- `ros2_ws/src/week07_08_my_package/` (kogu pakett koos failidega)
- parandatud `package.xml` ja `setup.py`
- README “Tulemused” sektsioon täidetud

### Käsud esitamiseks (git)
```bash
git status
git add -A
git commit -m "Week 07-08: create and configure ament_python package"
git push
```
