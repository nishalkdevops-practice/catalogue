#!groovy 
@Library('roboshop-shared-library') _

def configMap = [
    application: "nodeJSVM" ,
    component: "catalogue"
]
env

//  this is .groovy file name and function inside it 


if ( ! env.BRANCH_NAME.equalsIgnoreCase('master')){
    pipelineDecission.decidepipeline(configMap)

}
else{
    echo "master prod deployment should happen through the CR process"
}
