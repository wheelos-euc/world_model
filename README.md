# WheelOS World Model

Independent `wheelos_world_model` capability module containing `lane`,
`traffic_light`, `storytelling`, and the temporal/local-map `world_model`.
These remain separate Bazel targets and runtime components: visual observations,
scene facts, and temporal world state are not one algorithm or process.

The source layout, C++ includes and Proto import paths retain `modules/...`.
Components and tests remain individually selectable; sharing a package does
not merge runtime processes or require every GPU model to be built.

Use the mapped non-root managed container. From this checkout, run
`bazelisk cquery --config=dev -c opt //modules/world_model/local_map:local_scene_builder`; the Apollo product uses
`@wheelos_world_model//modules/...` through opt-in development overrides.
Live vehicle/map/model selection belongs to deployment configuration.
Workspace-wide defaults live in the product's `conf/`, not in this package.

Use `//modules/lane/...`, `//modules/traffic_light/...`, or
`//modules/storytelling/...` for individual components. The aggregate
`//:install_dir` includes GPU components and needs their existing SDKs.
Traffic Light still consumes legacy Perception graph/inference helpers; package
co-location does not remove that transition dependency.

SDK installs apply `third_party/rules_pkg/execroot_runfiles.patch`.
Consuming roots must carry that override; dependency-root overrides do not apply.
This ignored checkout must accompany product changes. Its Git source is
registered in `wheelos.repos`; no Bzlmod registry release has been published.

Configured CPU analysis is not GPU inference acceptance. GPU targets
retain their CUDA/TensorRT/model requirements; broad unconfigured
queries may load disabled or legacy backend repositories.
