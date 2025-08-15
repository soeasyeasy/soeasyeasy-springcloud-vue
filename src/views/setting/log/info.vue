<template>
	<el-main style="padding: 0 20px">
		<el-descriptions :column="1" border size="small">
			<el-descriptions-item label="类名">{{
				data.className
			}}</el-descriptions-item>
			<el-descriptions-item label="请求接口">{{
				data.requestUri
			}}</el-descriptions-item>
			<el-descriptions-item label="请求方法">{{
				data.methodName
			}}</el-descriptions-item>
			<el-descriptions-item label="请求方式">{{
				data.method
			}}</el-descriptions-item>
			<el-descriptions-item label="用户">{{
				data.user
			}}</el-descriptions-item>
			<el-descriptions-item label="客户端IP">{{
				data.clientIp
			}}</el-descriptions-item>
			<el-descriptions-item label="日志时间">{{
				data.startTime
			}}</el-descriptions-item>
			<!-- <el-descriptions-item label="入参">{{data.args}}</el-descriptions-item>
			<el-descriptions-item label="出参">{{data.result}}</el-descriptions-item> -->
		</el-descriptions>
		<el-collapse v-model="activeNames" style="margin-top: 20px">
			<!-- <el-collapse-item title="常规" name="1">
				<el-alert title="在没有配置的 DNS 服务器响应之后，名称 update-khd.2345.cc 的名称解析超时。" :type="typeMap[data.level]" :closable="false"></el-alert>
			</el-collapse-item> -->
			入参
			<el-input v-model="formattedArgs" style="padding: 15px" autosize type="textarea" placeholder="Please input"
				disabled="true" />
			出参
			<el-input v-model="formattedResult" style="padding: 15px" autosize type="textarea"
				placeholder="Please input" disabled="true" />
			<el-collapse-item title="详细" name="2">
				<div class="code">
					Request: { User-Agent: "Mozilla/5.0 (Windows NT 10.0; WOW64)
					AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198
					Safari/537.36" }, Response: { Content-Type:
					"application/json; charset=utf-8", Date: "Fri, 25 Jun 2021
					03:02:14 GMT", Server: "nginx/1.17.8" }
				</div>
			</el-collapse-item>
		</el-collapse>
	</el-main>
</template>

<script>
export default {
	data() {
		return {
			data: {},
			activeNames: ["1"],
			typeMap: {
				info: "info",
				warn: "warning",
				error: "error",
			},
		};
	},
	computed: {
		formattedArgs() {
			return this.formatJson(this.data.args);
		},
		formattedResult() {
			return this.formatJson(this.data.result);
		},
	},
	methods: {
		formatJson(jsonStr) {
			if (!jsonStr) return "null";

			try {
				// 如果已经是对象，直接格式化
				const obj =
					typeof jsonStr === "string" ? JSON.parse(jsonStr) : jsonStr;
				return JSON.stringify(obj, null, 2); // 格式化，缩进 2 个空格
			} catch (e) {
				return `Invalid JSON: ${jsonStr}`;
			}
		},
		setData(data) {
			this.data = data;
		},
	},
};
</script>

<style scoped>
.code {
	background: #848484;
	padding: 15px;
	color: #fff;
	font-size: 12px;
	border-radius: 4px;
}
</style>
