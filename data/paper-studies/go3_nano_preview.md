# RoboDojo GO-3 Nano Preview 调研（公开证据快照）
> 访问/整理日期：2026-10-30（Asia/Tokyo）。对象必须与发布会的 **GO-3 Preview** 区分：榜单条目是 **GO-3 Nano Preview**。以下只把公开事实写成事实；推断明确标注。
## 榜单总览
RoboDojo 官方仿真榜将 GO-3 Nano Preview 标为 **Agent + WAM**，当前 agent track 第一。官方嵌入数据生成时间为 2026-10-29T14:44:43.743Z，新闻记录于 2026-10-27 收录。榜单 headline 仍写 42 个仿真任务；逐任务表和 rollout manifest 暴露 54 个 key（含 `_random`、`_by_language` 变体）。

|排名|方法|类型|贡献方|Average score / SR|
|---:|---|---|---|---:|
|1|GO-3 Nano Preview|Agent + WAM|AGIBOT|61.90 / 56.42%|
|2|PyRUA-Lean|Agent|PKU DAGroup|55.26 / 50.35%|
|3|HexaShell-Preview|Agent|HexaFuture|53.18 / 46.85%|
|4|WorldScape-R²SI|Agent + WAM|Manifold AI|46.58 / 39.35%|
|5|EmbodiedEvo|Agent|Einsia.AI|45.08 / 38.95%|
|6|PhysicalRSI|Agent + VLA|HKU MMLab & KAI|36.27 / 31.38%|
|7|GPT-6-Astra|Agent|RoboDojo Team|28.97 / 22.48%|
|8|DeepSeek-Flash|Agent|RoboDojo Team|2.99 / 1.92%|
|9|GPT-5.5|Agent|RoboDojo Team|1.13 / 0.88%|

GO-3 相对第二名 PyRUA-Lean 高 6.64 score points；它在 precision、long-horizon、open 三项最高，但 memory 低于 HexaShell-Preview 和 EmbodiedEvo，standard/random generalization 也不是最高。

## GO-3 的公开方法证据

|字段|公开证据|边界|
|---|---|---|
|目标|AGIBOT 称 GO-3 Preview 是下一代 embodied foundation model，用于统一推理、预测、动作，预测动作后果、适应变化并泛化到未见任务序列。|没有 Nano 专属论文或规格。|
|输入/输出|榜单类型为 Agent + WAM；可保守推断为视觉/任务观察与指令到机器人动作。|AGIBOT 未公开输入 schema、tokenizer、action chunk、频率、维度；推断不应当写成已证实接口。|
|数据处理|发布稿称 pre-training、post-training、部署后持续改进；提及 AGIBOT WORLD 2026、MEgo、Genie Sim 3.0。|无 GO-3 专属数据量、清洗、混合比例、loss 或 compute。|
|Agent loop|发布稿给出 data–model–robot–scenario deployment loop：真实任务反馈进入模型/工作流更新。|无公开 replanning cadence、工具调用、重试/恢复策略。|
|WAM/VLA/记忆|官方榜单标签 Agent + WAM；架构名 WRAM。|RoboDojo 的 Memory 是评测维度，不等于模型拥有外部 memory；未见 GO-3 的检索库、工具 API 或 VLA action head 规格。|
|训练/自进化|AGIBOT 的 Physical Intelligence Scaling = pre-training + post-training + deployment 后持续改进；另有 AGILE 自演化 agent 的发布描述。|不能据此断言 AGILE 机制就是 GO-3 Nano 的在线算法。|
|评测|RoboDojo 仿真榜 5 个能力维度（generalization、precision、long-horizon、memory、open）和单独 SR；官方 repo 说明总 benchmark 为 42 sim + 18 real。|GO-3 当前条目是仿真；没有公开 real-world GO-3 Nano 分数。|

## GO-3 分数与失败剖面

|维度|Score|SR|
|---|---:|---:|
|Average|61.90|56.42%|
|Avg. (w/o Open)|61.95|56.71%|
|Generalization（标准）|45.93|43.00%|
|Generalization（random）|26.97|24.33%|
|Precision|78.65|76.00%|
|Long-Horizon|68.21|53.50%|
|Memory|64.50|63.67%|
|Open|61.71|55.25%|

### 逐任务证据

下表的 `score/SR` 来自官方 leaderboard 的 per-task 数据；`rollout 6片段` 来自官方 manifest，仅用于指出公开片段的成功/失败，不是榜单分母。

|维度|任务|score / SR|公开片段（success/fail）|
|---|---|---:|---:|
|open|`align_blocks`|88.00 / 88.00%|5/1|
|generalization|`arrange_largest_number`|82.60 / 76.00%|3/3|
|variant|`arrange_largest_number_random`|53.00 / 48.00%|2/4|
|precision|`build_tower`|100.00 / 100.00%|6/0|
|long_horizon|`classify_objects`|79.70 / 72.00%|4/2|
|open|`classify_objects_by_language`|74.60 / 66.00%|5/1|
|memory|`cover_blocks`|100.00 / 100.00%|6/0|
|precision|`deposit_coin`|54.00 / 48.00%|2/4|
|precision|`fasten_screws`|96.40 / 94.00%|6/0|
|long_horizon|`fill_egg_holder`|5.40 / 0.00%|0/6|
|long_horizon|`fill_pen_holder`|17.80 / 4.00%|0/6|
|generalization|`fold_clothes`|66.40 / 60.00%|5/1|
|variant|`fold_clothes_random`|42.40 / 32.00%|2/4|
|open|`general_pickup`|16.00 / 16.00%|2/4|
|generalization|`hang_mugs`|3.00 / 0.00%|0/6|
|variant|`hang_mugs_random`|1.20 / 0.00%|0/6|
|memory|`imitate_sorting_sequence`|27.00 / 22.00%|0/6|
|precision|`insert_key`|41.60 / 32.00%|4/2|
|precision|`insert_tubes`|95.20 / 92.00%|6/0|
|long_horizon|`make_kong`|100.00 / 100.00%|6/0|
|generalization|`make_toast`|3.00 / 0.00%|0/6|
|variant|`make_toast_random`|3.00 / 0.00%|0/6|
|memory|`match_and_pick_from_conveyor`|28.00 / 28.00%|4/2|
|long_horizon|`organize_table`|74.00 / 16.00%|0/6|
|generalization|`pack_objects_into_box`|8.60 / 0.00%|0/6|
|variant|`pack_objects_into_box_random`|3.80 / 0.00%|0/6|
|open|`pick_from_conveyor_by_image`|0.00 / 0.00%|0/6|
|precision|`play_Xylophone`|100.00 / 100.00%|6/0|
|long_horizon|`play_stacking_toy`|78.40 / 52.00%|0/6|
|long_horizon|`play_tic_tac_toe`|100.00 / 100.00%|6/0|
|precision|`plug_in_charger`|70.00 / 70.00%|4/2|
|precision|`pour_balls_into_vase`|72.00 / 72.00%|4/2|
|open|`pour_by_language`|100.00 / 100.00%|6/0|
|generalization|`pour_liquid_into_cup`|36.00 / 36.00%|2/4|
|variant|`pour_liquid_into_cup_random`|4.00 / 4.00%|0/6|
|memory|`press_by_number`|100.00 / 100.00%|6/0|
|generalization|`push_T`|72.00 / 72.00%|5/1|
|variant|`push_T_random`|64.00 / 64.00%|4/2|
|long_horizon|`put_bottles_into_dustbin`|90.40 / 84.00%|4/2|
|open|`solve_equation`|82.00 / 82.00%|5/1|
|generalization|`sort_nesting_dolls_by_size`|80.00 / 80.00%|5/1|
|variant|`sort_nesting_dolls_by_size_random`|8.00 / 8.00%|0/6|
|generalization|`stack_blocks`|100.00 / 100.00%|6/0|
|open|`stack_blocks_by_language`|81.60 / 80.00%|4/2|
|variant|`stack_blocks_random`|79.60 / 76.00%|4/2|
|generalization|`stack_bowls`|93.20 / 92.00%|6/0|
|variant|`stack_bowls_random`|63.00 / 60.00%|2/4|
|generalization|`store_laptop_and_headphones`|6.40 / 0.00%|0/6|
|variant|`store_laptop_and_headphones_random`|1.60 / 0.00%|0/6|
|open|`store_tools_in_toolbox`|51.50 / 10.00%|0/6|
|memory|`swap_T`|96.00 / 96.00%|5/1|
|memory|`swap_blocks`|36.00 / 36.00%|4/2|
|generalization|`sweep_blocks`|0.00 / 0.00%|0/6|
|variant|`sweep_blocks_random`|0.00 / 0.00%|0/6|

总体 manifest：54 个任务 key、324 个片段，156 success / 168 fail；全部标注 `arx_x5`。这 6 clips/task 是展示性 rollout evidence，不能反推 56.42% 的正式 SR。

## 可复现字段与缺口

- **已复现字段**：官方模型名、贡献方、类型、榜单分数/SR、5 维分数、54 个任务 key 的 score/SR、manifest 中 task/robot/clip key/outcome。
- **可观看 rollout**：将 manifest 的 `key` 拼到 `https://media.luminis-sim.com/`；例如 [align_blocks success clip](https://media.luminis-sim.com/robodojo_eval_videos/align_blocks/GO-3%20Nano%20Preview/arx_x5/3_ckpt_name=go3-preview%2Caction_type=joint/go3-preview-s3-w7-align_blocks-L0-55-1792903945/episode_0000000_cam_head_success.mp4)。
- **尚不可复现**：GO-3 Nano checkpoint/source、部署容器、精确 prompt、工具/记忆配置、相机与 action schema、seed/episode denominator、训练数据/compute。
- **事实/推断边界**：WRAM、Physical Intelligence Scaling、deployment loop 是 AGIBOT 对 GO-3 Preview 家族的公开描述；Nano 专属实现细节仍是未知。

## 来源

1. [RoboDojo 官方仿真榜](https://robodojo-benchmark.com/leaderboard?bench=sim)（榜单、维度、逐任务表、收录日期）。
2. [RoboDojo rollout manifest](https://robodojo-benchmark.com/data/rolloutManifest.generated.json) 与 [GO-3 rollout browser](https://robodojo-benchmark.com/leaderboard/rollouts/GO-3%20Nano%20Preview?bench=sim)。
3. [RoboDojo 官方仓库](https://github.com/robodojo-benchmark/RoboDojo)（42 sim / 18 real、五维、XPolicyLab）。
4. [AGIBOT 官方发布稿](https://www.agibot.com/article/231/detail/131.html)（WRAM、zero/few-shot、Physical Intelligence Scaling、deployment loop）。
5. [RoboDojo leaderboard protocol](https://robodojo-benchmark.com/leaderboard/protocol)。
