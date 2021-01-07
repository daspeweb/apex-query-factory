Exemplos:        
        
DW_QueryFactory.get('Opportunity')
    .setCondition(DW_QueryCondition.newInstance('StageName', '=', 'Fechado/Ganho'))
    .run();

DW_QueryFactory.get('Opportunity')
    .setCondition(DW_QueryCondition.newInstance('StageName', '=', 'Fechado/Ganho'))
    .setOrCondition(DW_QueryCondition.newInstance('StageName', '=', 'Fechado/Perdido'))
    .run();

DW_QueryFactory.get('Opportunity')
        .setCondition(DW_QueryCondition.newInstance('StageName', new List<String>{'Fechado/Ganho', 'Fechado/Perdido'}))
        .run();

DW_QueryFactory.get('Opportunity')
        .setCondition(DW_QueryCondition.newInstance('StageName', '=', 'Fechado/Ganho'))
        .setCondition(DW_QueryCondition.newInstance('Amount', '>', 50000))
        .run();


DW_QueryFactory.get('Opportunity')
        .setCondition(DW_QueryCondition.newInstance('CloseDate', '>', System.today().addDays(-300)))
        .run();

DW_QueryFactory.get('Opportunity')
.setCondition(DW_QueryCondition.newInstance('StageName', '=', 'Fechado/Ganho'))
.setGroupedCondition(DW_QueryConditionComposition.setConditionList(
        new List<DW_QueryCondition>{
            DW_QueryCondition.newInstance('Amount', '<', 5000),
            DW_QueryCondition.newInstance('Amount', '>', 50000, DW_OperatorOptions.OR_OPERATOR)
        }, null
))
.setGroupedCondition(DW_QueryConditionComposition.setConditionList(
        new List<DW_QueryCondition>{
                DW_QueryCondition.newInstance('Amount', '>', 20000),
                DW_QueryCondition.newInstance('Amount', '<', 30000, DW_OperatorOptions.AND_OPERATOR)
        }, null
)).run();


DW_QueryFactory.get('Opportunity')
    .setCondition(DW_QueryCondition.newInstance('StageName', '=', 'Fechado/Ganho'))
    .with('OpportunityLineItems', 'OpportunityLineItem')
    .limitedTo(10)
    .run();
