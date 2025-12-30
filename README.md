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

---
## Ülesanne B: muuda metaandmeid (kohustuslik)

`package.xml` ja `setup.py` on ROS 2 paketi jaoks üliolulised failid, mis sisaldavad selle metaandmeid. Testimissüsteem kontrollib, et sa oled need korrektselt täitnud.

1)  Ava `package.xml` (`.../week07_08_my_package/package.xml`)
2)  Täida väljad `description`, `maintainer` (nimi) ja `maintainer_email`.

    ```xml
    <!-- Näide -->
    <description>My awesome ROS 2 package for week 7-8.</description>
    <maintainer email="sinu.nimi@email.com">Sinu Nimi</maintainer>
    <license>Apache-2.0</license>
    ```

3)  Ava `setup.py` (`.../week07_08_my_package/setup.py`)
4)  Täida samad väljad ka siin.

    ```python
    # Näide
    setup(
        # ...
        maintainer='Sinu Nimi',
        maintainer_email='sinu.nimi@email.com',
        description='My awesome ROS 2 package for week 7-8.',
        license='Apache-2.0',
        # ...
    )
    ```

---
## Ülesanne C: ehita ja käivita (kohustuslik)

1)  Mine oma workspace’i **juurkausta** (NB! Mitte `src` kausta).
    *   **IDX-is:** `cd /workspace/ros2_ws`
    *   **Docker Desktopis:** `cd ~/ros2_ws`

2)  Ehita (`build`) oma uus pakett `colcon` abil. See kompileerib koodi ja teeb selle ROS-ile kättesaadavaks.

    ```bash
    colcon build --packages-select week07_08_my_package
    ```
    Kui ehitamine õnnestub, näed teadet `Finished <<< week07_08_my_package`.

3)  Aktiveeri (`source`) oma workspace. See on **ÄÄRMISELT OLULINE** samm, mis tuleb teha **IGAS UUES TERMINALIS**, kus sa tahad oma koodi käivitada. Ilma selleta ei leia ROS sinu paketti.

    ```bash
    source install/setup.bash
    ```
    *Vihje: selle käsu saab lisada oma terminali seadistusfaili (`~/.bashrc`), et see automaatselt käivituks.*

4)  Käivita (`run`) oma node.

    ```bash
    ros2 run week07_08_my_package my_node
    ```

    Kui kõik on õigesti tehtud, peaks terminali ilmuma teade:
    `Hi from week07_08_my_package.`

---

## Esitamise kord

Harjutuse edukaks esitamiseks **pead töötama oma isiklikus GitHub Classroomi repos**, mis on loodud selle nädala jaoks.

1.  **Ava ülesande link Moodle'ist:**
    - Mine kursuse Moodle'i lehele.
    - Leia sealt selle nädala (Week 07-08) ülesande juurest link oma isikliku GitHub Classroomi repositooriumi loomiseks.

2.  **Klooni enda isiklik repo GitHubist**, mille nimi sisaldab sinu GitHubi kasutajanime.
    Näide:
    ```bash
    git clone https://github.com/Tallinna-Tehnika-korgkool/TRO029-week07-08_workspace-<sinu_kasutajanimi>
    ```

3.  **Tee kõik ülesanded selles kloonitud repos.**

4.  **Lisa ja `commit`'i oma muudatused** (`ros2_ws` kaust koos sinu paketiga).
    ```bash
    git add .
    git commit -m "docs: Complete week 7-8 exercise"
    git push
    ```

5.  Kui `push` on tehtud, käivituvad **automaatsed testid** (GitHub Actions) sinu repo **Actions** vahekaardil.
    - ✅ **Roheline** ✔️ tähendab, et kõik on korras.
    - ❌ **Punane** ✖️ tähendab, et midagi on puudu või valesti – paranda ja tee uus `commit` ja `push`.

> **NB!** Kui töötad väljaspool oma isiklikku Classroom repo't, siis testid ei tööta ja harjutust ei loeta esitatuks.
