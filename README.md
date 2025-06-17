# Strapi v5 examples


## Controllers

### Controller with context types:

```javascript
import { factories } from '@strapi/strapi';
import { Context } from 'koa';

export default factories.createCoreController('api::process.process', {
  async create(ctx: Context) {
    try {
      const process = await strapi.documents('api::process.process').create({
        data: ctx.request.body.data,
        status: 'published',
      });

      ctx.created({ data: process, meta: {} });
    } catch (error) {
      const errorMessage = error.message ?? 'Invalid payload';
      strapi.log.error('Create error', errorMessage);
      ctx.badRequest(errorMessage);
      return;
    }
  },
});
```

### Controller with update param:

```javascript
import { factories } from '@strapi/strapi';
import { Context } from 'koa';

export default factories.createCoreController('api::process.process', {
  async update(ctx: Context) {
    try {
      const processDocumentId = ctx.params.id;
      
      ...
      ctx.ok({ data: process, meta: {} });
    } catch (error) {
      const errorMessage = error.message ?? 'Invalid payload';
      strapi.log.error('Update error', errorMessage);
      ctx.badRequest(errorMessage);
      return;
    }
  },
});
```
