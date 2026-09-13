/* Greek To Go Taverna POS — freshness service worker */

self.addEventListener('install', () => {
  self.skipWaiting();
});

self.addEventListener('activate', (event) => {
  event.waitUntil(
    caches.keys()
      .then(keys => Promise.all(keys.map(key => caches.delete(key))))
      .then(() => self.clients.claim())
  );
});

self.addEventListener('fetch', (event) => {
  const request = event.request;

  if (request.method !== 'GET') return;

  const url = new URL(request.url);

  const isNavigation = request.mode === 'navigate';

  const isPosHtml =
    url.origin === self.location.origin &&
    (
      url.pathname.endsWith('/greektogotavernaPOS/') ||
      url.pathname.endsWith('/greektogotavernaPOS/index.html')
    );

  if (isNavigation || isPosHtml) {
    event.respondWith(
      fetch(
        new Request(request, {
          cache: 'no-store'
        })
      ).catch(() => fetch(request))
    );
  }
});
