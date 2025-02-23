---
sidebar_position: 8
---

# Guards

To access the `I18nContext` inside your guards use the `getI18nContextFromRequest` helper function.

```typescript title="src/test.guard.ts"
import { CanActivate, ExecutionContext, Injectable } from "@nestjs/common";
import { Observable } from "rxjs";
import { resolveI18nContextFromRequest } from "nestjs-i18n";

@Injectable()
export class TestGuard implements CanActivate {
  canActivate(
    context: ExecutionContext,
  ): boolean | Promise<boolean> | Observable<boolean> {
    const request = context.switchToHttp().getRequest();
    let response = context.switchToHttp().getResponse();

    const i18n = getI18nContextFromRequest(request)
    console.log('current language', i18n.lang);

    return true;
  }
}
```

:::warning

This only works when running in an `http` context! So it works with `express`, `fastify` and `graphql` (most parts).

:::