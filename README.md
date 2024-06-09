# 学振PD審査員の方々へ
本githubページでは、公開するオープンソースソフトウェアに加えて、申請書提出以降で確定した成果を期間限定で掲載します。
## 申請者がメイン講師となるセミナー
- 株式会社テクノセンターが主催するセミナーのWEBページ (https://www.j-techno.co.jp/seminar/seminar-63357/)
   -  申請書8ページの「(1) 研究に関する自身の強み」における「2. 技量」での内容

<br><br><br>
------------  Please see the following contents for a user of this software.  ------------
# Introduction
The full linear wheel odometry factor is a constraint depending on not only robot poses but also the kinematic parameters of a skid-steering robot.
This factor can be used for two- and six-wheeled robots and tracked robots other than four-wheeled robots if these robots don't have steering mechanisms.
The kinematic parameters are defined by the full linear model. 
Therefore, this factor performs online calibration of kinematic models for skid-steering robots in addition to the motion constraint.
**Owing to the online calibration, reliable wheel odometry-based constraint being adaptive to unknown environments (especially, slippage depending on the type of ground surface) is enabled without prior offline calibration manually**.

The main contribution of this factor is two-fold.
* Online calibration of kinematic parameters for skid-steering robots
    * Skid-steering robot's wheel odometry depends on directly-nonobservable phenomena or values (e.g., wheel slippage, and kinematic model errors caused by tire pressure and  aging).
    * This factor can calibrate the above parameters online.
* Reliable motion constraints
    * Wheel odometry is accurately calculated based on the online calibration.
    * This factor makes an odometry estimation (e.g., LiDAR-IMU odometry) more robust to environments where point clouds degenerate (e.g., long corridors and tunnels).

The following video validates that LiDAR-IMU odometry with our full linear wheel odometry factor accomplishes accurate odometry estimation even in long corridors.
[[video #1 with voice](https://youtu.be/PHIXTPku_Uo)], [[video #2 without voice](https://www.youtube.com/watch?v=woLl1c5IenE)]
# Prerequisited
* [GTSAM](https://github.com/borglab/gtsam/tree/4.2a9)

We tested this code by Ubuntu 22.04

# Usage
**The full linear wheel odometry factor is implemented as a header-only file written in C++. Therefore, you can use this factor by only including this header file in your code.** Please refer to the examples directory for how to incorporate this factor into your factor graph defined by GTSAM. Specifically, the example file can be executed based on the following commands.
```commandline
cd examples/
cmake .
make
./full_linear_wheel_odometry_factor_example
```

<!-- # Citation
If you use the full linear wheel odometry factor for academic work, please cite the following publication.  -->
