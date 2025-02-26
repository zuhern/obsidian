---
Created: Invalid date
Updated: Invalid date
---
auth.js/registerif (randomKey[phoneNumber] === inputKey) { debug("correct key!"); delete randomKey[phoneNumber]; } else { debug('incorrect key'); return next(new UnauthorizedAccessError('401', getCode('auth', '2'))); }이부분.. 계정 처음 생성할 때 에러남