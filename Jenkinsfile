#!/usr/bin/groovy
/*
 * Copyright 2016 Red Hat, Inc.
 *
 * Red Hat licenses this file to you under the Apache License, version
 * 2.0 (the "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
 * implied.  See the License for the specific language governing
 * permissions and limitations under the License.
 */
@Library('github.com/rawlingsj/fabric8-pipeline-library@master')
def dummy
mavenNode {
  dockerNode {
    checkout scm
    sh "git remote set-url origin git@github.com:fabric8io/fabric8-maven-plugin.git"

    def pipeline = load 'release.groovy'

    stage 'Stage'
    def stagedProject = pipeline.stage()

    // stage 'Approve'
    // pipeline.approveRelease(stagedProject)

    stage 'Promote'
    pipeline.release(stagedProject)

    stage 'Update downstream dependencies'
    pipeline.updateDownstreamDependencies(stagedProject)
  }
}
