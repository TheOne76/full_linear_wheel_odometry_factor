# 学振PD審査員の方々へ
本githubページでは、公開するオープンソースソフトウェアに加えて、申請書提出以降で確定した成果を10月まで掲載します。
## 申請者がメイン講師となるセミナー
- 株式会社テクノセンターが主催するセミナーのWEBページ (https://www.j-techno.co.jp/seminar/seminar-63357/)
   -  ページを開くのに40秒ほどかかる場合があります。
   -  申請書8ページの「(1) 研究に関する自身の強み」における「2. 技量」で言及されている内容です。
## 特別研究員－ＤＣの採用最終年次における研究奨励金特別手当の支給対象者に決定
- 特別研究員－ＤＣの採用最終年次の在籍者のうち、**採用期間中に優れた研究成果を上げ**、さらなる進展が期待される者が支給対象です。
- 特別研究員及び受入研究者の**研究報告書（研究成果の報告に加え、提案手法のソースコードの公開や論文発表数など）** を基に、外部有識者により構成される特別研究員等審査会による審議で決定されました。
## 筆頭著者での新しい学術論文の投稿（7月9日投稿、査読中）
**Taku Okawara**, Kenji Koide, and Shuji Oishi, Masashi Yokozuka, Atsuhiko Banno, Kentaro Uno and Kazuya Yoshida: “Tightly-Coupled LiDAR-IMU-Wheel Odometry with an Online Neural Kinematic Model Learning via Factor Graph Optimization”, Robotics and Autonomous Systems, 2024
- **[preprintで公開中](https://drive.google.com/file/d/1_JK0vcv3zrz5MDR25WO1yYEQS61o-sfG/view?usp=drive_link)**
- ロボットの運動学を線形モデル（申請書における[成果8]）から**非線形モデル（ニューラルネットワーク）へと拡張したモデルを推定システムに統合**することで、従来の自己位置推定を凌駕する結果を得ました。
- **ロボット分野でのトップジャーナル**に投稿しました。
   - Google scholarでのh5指標でトップ14位のジャーナル [[link](https://scholar.google.co.jp/citations?view_op=top_venues&hl=ja&vq=eng_robotics)]
   - ![Google scholar RAS](https://github.com/TakuOkawara/full_linear_wheel_odometry_factor/assets/105478884/1a280403-92c9-4351-b5f3-85564434bf5d)
<br><br><br>




------------  Please see the following contents for a user of this software.  ------------

# Cite
Please cite the following paper when you use this code for academic work.

Note that the "journal={arXiv...}" part will be replaced with a proper one when this paper review is accepted.

Link: https://arxiv.org/pdf/2404.02515

---

   @article{okawara2024tightly,
     title={Tightly-Coupled LiDAR-IMU-Wheel Odometry with Online Calibration of a Kinematic Model for Skid-Steering Robots},
     author={Okawara, Taku and Koide, Kenji and Oishi, Shuji and Yokozuka, Masashi and Banno, Atsuhiko and Uno, Kentaro and Yoshida, Kazuya},
     journal={arXiv preprint arXiv:2404.02515},
     year={2024}
     }
  
---


# Introduction
The full linear wheel odometry factor is a constraint depending on not only robot poses but also the kinematic parameters of a skid-steering robot.
This factor can be used for two- and six-wheeled robots and tracked robots other than four-wheeled robots if these robots don't have steering mechanisms.
The kinematic parameters are defined by the full linear model (Please see the following image for understanding this model). 

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

## Overview of the full linear model
![image](https://github.com/TakuOkawara/full_linear_wheel_odometry_factor/assets/105478884/8b0ccedf-ddc3-4b89-bcc0-0620664b69c8)


# Prerequisited
* [GTSAM](https://github.com/borglab/gtsam/tree/4.2a9)

We tested this code by Ubuntu 22.04

# Usage
**The full linear wheel odometry factor is implemented as a header-only file written in C++. Therefore, you can use this factor by only including this header file in your code.** Please refer to the [examples](https://github.com/TakuOkawara/full_linear_wheel_odometry_factor/tree/main/examples) directory for how to incorporate this factor into your factor graph defined by GTSAM. Specifically, the example file can be executed based on the following commands.
```commandline
cd examples/
cmake .
make
./full_linear_wheel_odometry_factor_example
```

<!-- # Citation
If you use the full linear wheel odometry factor for academic work, please cite the following publication.  -->
