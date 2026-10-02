# TranslateFlow Dictionary Builder

TranslateFlow 的独立离线词典构建工程：来源数据 → SQLite 中间库 → 义项与词形编译 → HTML → MDX/MDD。

## 当前状态

**Audited prototype / NOT RELEASE READY。** 本仓库从本会话交付的 v3 构建器迁入，不是已修复或已认证的词典发布版本。已知 F01–F09 缺陷仍待修复；原有 5 个测试通过并不证明语义正确或最终二进制可用。

后续源码、审核证据与开发任务以此仓库为准，不再以聊天中的 ZIP 文件作为更新渠道。浏览器扩展继续独立维护在 `CoderLambert/translateflow-plugin`；本仓库不复制插件运行时，也不修改其权限或安全限制。

## 开发入口

- `AGENTS.md`：执行规则、边界与验证标准。
- `docs/PLAN.md`：当前唯一优先阶段与交付条件。
- `docs/audit/v3/AUDIT.md`：v3 审核报告。
- `docs/audit/v3/reproduce_findings.py`：历史缺陷诊断探针（不是发布验收测试）。
- `docs/BASELINE.md`：迁入来源、文件校验与实际验证范围。
- `docs/history/README-v3.md`：原始使用说明；不能覆盖当前审核结论。

## 本地开始

```bash
git clone https://github.com/CoderLambert/translateflow-dictionary-builder.git
cd translateflow-dictionary-builder
PYTHONPATH=src python3 -m unittest discover -s tests -v
python3 docs/audit/v3/reproduce_findings.py "$PWD"
```

Python 3.11+。上述测试使用合成数据，不下载词典、安装第三方包或调用 AI。诊断探针会报告现有错误行为；正常退出不代表缺陷已修复。

原型构建入口 `build.sh` 暂时保留，**不作为推荐发布命令**。它会联网下载来源并构建词典，且仍受上述缺陷影响。阶段 A 完成前不要据此发布大词库或宣称达到牛津词典质量。

## 下一项交付

先修复词义错误合并、词形方向、同义词丢失、事务/缓存/别名以及验证误报，交付 50–100 个代表性真实词的可导入 MDX/MDD、校验值和真实验证记录。随后再进行义项级质量实验与 5k 实用包，暂不追求 100k/200k 规模。

## 数据边界

仓库只保存代码、配置、说明和合成测试；原始词典、下载缓存、SQLite、API 密钥、生成的 MDX/MDD 及音频/字体资源不提交 Git。真实来源必须保留出处与版本；生成内容不得冒充原始词典事实。
