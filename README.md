REPRO STEPS:
1. `npx playwright install`
2. `npx playwright test --shard=1/2`
3. Move `reports/blobs/report-1.zip` to a temporary directory, so it isn't deleted by the next test run.
4. `npx playwright test --shard=2/2`
5. Move `report-1.zip` back into the `reports/blobs` directory.
6. `npx playwright merge-reports --config merge.config.ts ./reports/blobs`
7. Observe the `time` under `testsuites` in the merged junit report `reports/merged/report.xml`

Expected Result: `time="3.729"` The approximate total test time (with some floating point error)

Actual Result: `time="0.025825..."` Reported time is much lower than expected. Possibly the time the reports took to merge.
