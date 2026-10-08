# agentic-sdlc — DIY Agentic SDLC (no platform needed)

Port.io 없이 에이전트 스킬 조합으로 돌리는 agentic SDLC 파이프라인.

## 구성
- `catalog.yaml` — 사실의 원천. 서비스별 repo 경로, owner, tier, runbook,
  의존성, 배포 방식, `last_deploy`, `open_incidents`. 매 실행 시작 때 읽고
  끝날 때 갱신한다.
- `runbooks/` — 서비스별 운영 절차서. `_template.md`를 복사해서 채운다.
- `runs/` — 실행 로그 (감사 추적). `YYYY-MM-DD-HHMM-<slug>.md`.
- `.claude/skills/sdlc-runner/` — 오케스트레이터 스킬. Claude Code가 자동 인식.

## 파이프라인 (11단계)
1. 서비스 컨텍스트 조회 → 2. 요구사항 정리 → 3. 계획 수립
→ 4. 코드 작성 (ponytail 스킬)
→ 5. **게이트 1: 테스트/CI 실패 시 즉시 중단**
→ 6. 리뷰 + **게이트 2: 인간 승인 없이 배포 금지**
→ 7. 배포 → 8. 헬스 체크 → 9. 장애 대응 → 10. 피드백 환류 (catalog 갱신)

## 사용법
Claude Code에서: "SDLC 돌려줘" 또는 "agentic SDLC 파이프라인으로 이 기능 만들어줘"
