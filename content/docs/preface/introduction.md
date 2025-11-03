---
summary: "AdonisJS is a TypeScript-first web framework for Node.js. You can use it to create a full-stack web application or a JSON API server."
---

# Başlarken

::include{template="partials/introduction_cards"}

## AdonisJS Nedir?

AdonisJS is a TypeScript-first web framework for Node.js. You can use it to create a full-stack web application or a JSON API server.
AdonisJS, Node.js üzerinde çalışan TypeScript öncelikli web framework'tür. AdonisJS'i full-stack web uygulaması ya da JSON API Server geliştirmek için kullanabilirsiniz.

En temel haliyle, AdonisJS [uygulamanıza yapı saglar](../getting_started/folder_structure.md), [akıcı bir TypeScript geliştirme ortamı](../concepts/typescript_build_process.md) yapılandırır, backend kodunuz için [HMR](../concepts/hmr.md) yapılandırır, ve bolca iyi dökümente edilmiş ve sürekli güncelleme alan paketler sunar.

We envision teams using AdonisJS **spending less time** on trivial decisions like cherry-picking npm packages for every minor feature, writing glue code, debating for the perfect folder structure, and **spending more time** delivering real-world features critical for the business needs.
Hedefimiz AdonisJS kullanan ekiplerin her küçük özellik için uygun npm paketini seçmek, bunları birbirine bağlamak için ekstra kod yazmak ya da en iyi klasör yapılandırmasının nasıl olması gerektiğine dair tartışmalara **daha az zaman harcamaları** ve iş için kritik öneme sahip gerçek özellikleri geliştirmek için **zaman kazanmalarıdır**.

### Frontend agnostik

AdonisJS focuses on the backend and lets you choose the frontend stack of your choice.

Eğer basitlikten yanaysanız AdonisJS'i server'da statik HTML oluştumak için [geleneksel bir template motoruyla](../views-and-templates/introduction.md) kullanabilirsiniz, Vue/React uygulamanız için JSON API geliştirebilir ya da [Inertia](../views-and-templates/inertia.md) kullanarak favori frontend teknolojiniz ile mükemmel bir harmoni yakalayabilirsiniz.

AdonisJS sıfırdan sağlam bir backend geliştirmeniz için **her şey dahil** bir çözüm sunmayı hedefliyor. Email göndermek, kullanıcı girdilerini doğrulamak, CRUD işlemler yapmak ya da kullanıcı kimlik doğrulaması yapmak. Her şey dahil.

### Modern ve Type-safe

AdonisJS modern JavaScript primitives üzerine kuruldu. ES modules, Node.js sub-path import aliases, TypeScript kodunu çalıştırmak için SWC, ve asseet bundling için Vite kullanıyoruz.


Bunun yanında TypeScript, AdonisJS API'larının tasarımında da hatırı sayılır bir rol oynuyor. Mesela:

- [Type-safe event emitter](../digging_deeper/emitter.md#making-events-type-safe)
- [Type-safe environment variables](../getting_started/environment_variables.md)
- [Type-safe validation library](../basics/validation.md)

### MVC'yi benimsiyoruz

AdonisJS klasik MVC design pattern'i kullanıyor. Route'ları fonksiyonel JavaScript API kullanarak tanımlarsın, HTTP isteklerini yönetmek için işleyiş mantğını bir controller'da yazar ve route'a bağlarsın.

```ts
// title: start/routes.ts
import router from '@adonisjs/core/services/router'
const PostsController = () => import('#controllers/posts_controller')

router.get('posts', [PostsController, 'index'])
```

Controller'lar model'leri kullanarak veritabanından veri çekebilir ve yanıt olarak view (diğer adıyla template) oluşturabilirler. 

```ts
// dosya: app/controllers/posts_controller.ts
import Post from '#models/post'
import type { HttpContext } from '@adonisjs/core/http'

export default class PostsController {
  async index({ view }: HttpContext) {
    const posts = await Post.all()
    return view.render('pages/posts/list', { posts })
  }
}
```

Eğer API server geliştiriyorsanız view katmanını JSON yanıtıyla değiştirebilirsiniz. HTTP isteğini yönetme ve yanıtlama akışı aynı kalacak.

```ts
// dosya: app/controllers/posts_controller.ts
import Post from '#models/post'
import type { HttpContext } from '@adonisjs/core/http'

export default class PostsController {
  async index({ view }: HttpContext) {
    const posts = await Post.all()
    // delete-start
    return view.render('pages/posts/list', { posts })
    // delete-end
    // insert-start
    /**
     * Posts array'i otomatik olarak
     * JSON'a serialize edilecek
     */
    return posts
    // insert-end
  }
}
```

## Rehberdeki varsayımlar

AdonisJS dökümantasyonu referans rehberi olarak yazıldı. Ana ekip tarafından sunulan bazı paket ve modüllerin API kullanımlarını ele alıyor.

**Bu rehber size sıfırdan nasıl bir uygulama geliştiriliri öğretmeye çalışmıyor**. Eğer bu konuda ders arayışınız varsa [Adocasts](https://adocasts.com/)'den başlamanızı öneririz. Tom (Adocasts'in kurucusu) AdonisJS'deki ilk adımlarınızı destekleyecek yüksek kaliteli içerikler üretiyor.

Bu dökümantasyon mevcut modüllerin ve frameworkün iç işleyişi kapsamlı bir şekilde açıklıyor.

## Son sürümler
Aşağıda son yayınlanan sürümlerin listesi var. Bütün sürümleri görmek için [buraya tıkla](./releases.md).

::include{template="partials/recent_releases"}

## Sponsorlar

::include{template="partials/sponsors"}
