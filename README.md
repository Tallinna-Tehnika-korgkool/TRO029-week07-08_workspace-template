# Week 07–08: ROS 2 workspace ja Python pakett

Selle nädala eesmärk on õppida:
- kuidas luua ROS 2 Python pakett käsuga `ros2 pkg create`
- kuidas ehitada workspace’i `colcon`iga
- kuidas käivitada enda node `ros2 run` abil
- kuidas korrastada `package.xml` ja `setup.py` metaandmed (maintainer/description/license)

## Eeldused
- Sul töötab kursuse ROS 2 Humble keskkond (Docker/Devcontainer).
- Igas terminalis on ROS 2 sätitud (nt `source /opt/ros/humble/setup.bash`).

---

## ‼️ KÕIGE OLULISEM: Kus sa oma koodi hoiad?

**See on kõige sagedasem vea allikas.** Palun loe see hoolikalt läbi.

ÄRA AJAGA SEGAMINi kahte asja:

1.  **ROS 2 SÜSTEEMI KAUST (`/opt/ros/humble`):
    - **SEE EI OLE SINU TÖÖKAUST!**
    - See sisaldab ROS-i enda installatsiooni ja selle lähtekoodi (nt `/opt/ros/humble/src`).
    - **ÄRA IIALGI loo ega muuda faile selles kaustas!** See on süsteemne kaust ja sa rikud sellega oma ROS-i installatsiooni.

2.  **SINU ISIKLIK TÖÖKAUST (Workspace, nt `ros2_ws`):
    - **SEE ON KOHT, KUHU SA LOOD OMA KOODI.**
    - See on eraldi kaust, mille sa ise lood oma pakettide hoidmiseks.
    - Selle asukoht sõltub sinu keskkonnast:
        - **IDX-is:** Sinu töökaust on `/workspace`. Seega asub sinu workspace siin: `/workspace/ros2_ws`.
        - **Docker Desktopis:** Sinu töökaust on kodukataloog (`~`). Seega asub sinu workspace siin: `~/ros2_ws`.

**Kõik järgnevad käsud tuleb käivitada SINU ISIKLIKUS TÖÖKAUSTAS (`ros2_ws`), MITTE ROS-i süsteemses kaustas.**

---

## Ülesanne A: loo uus pakett (kohustuslik)

1) Loo ja mine oma workspace’i `src` kausta. Kui `ros2_ws` või `src` kausta pole, loo need `mkdir` käsuga.

   *   **IDX-is:**
       ```bash
       # Loo kaustad, kui neid pole
       mkdir -p /workspace/ros2_ws/src
       # Mine kausta
       cd /workspace/ros2_ws/src
       ```

   *   **Docker Desktopis:**
       ```bash
       # Loo kaustad, kui neid pole
       mkdir -p ~/ros2_ws/src
       # Mine kausta
       cd ~/ros2_ws/src
       ```

2) Loo uus Python pakett (kasuta **sama nime** nagu siin):
- paketi nimi: `week07_08_my_package`
- node nimi: `my_node`

```bash
# Veendu, et oled õiges kaustas (lõppema peaks .../ros2_ws/src)
ros2 pkg create --build-type ament_python --license Apache-2.0 --node-name my_node week07_08_my_package
```

Pärast seda peab sul tekkima kaust:

*   **IDX-is:** `/workspace/ros2_ws/src/week07_08_my_package`
*   **Docker Desktopis:** `~/ros2_ws/src/week07_08_my_package`
