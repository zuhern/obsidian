---
Created: Invalid date
Updated: Invalid date
---
}).state('main.proc.detail.proc-acts-edit', {

url: '/modeler/procs/:procId/:version/procacts/:actdefseq/usageType/:usageType',

onEnter: function (modalFactory, $stateParams) {

// 이전 버전 팝업 state: proc-acts

var params = {

procId: $stateParams.procId,

version: $stateParams.procVersion,

actdefseq: $stateParams.actSeq

};

var targetHtml = 'views/stnd-mng/modeler-app/proc-acts.html';

var targetCtrl = 'ProcActsController as actCtrl';

modalFactory.open('md', targetHtml, targetCtrl, params);

},