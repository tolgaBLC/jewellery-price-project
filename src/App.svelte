<script>
  import { Styles, Col, Row, Input, Card, CardBody } from "sveltestrap";
  import { alis } from "./stores.js";
  import { satis } from "./stores.js";
  import EskiCeyrek from "./EskiCeyrek.svelte";
  import { fade } from "svelte/transition";
  import YeniCeyrek from "./YeniCeyrek.svelte";
  import Bilezik from "./Bilezik.svelte";
  import AtaLira from "./AtaLira.svelte";
  import ResatLira from "./ResatLira.svelte";
  import BirGram from "./BirGram.svelte";
  import YarimGram from "./YarimGram.svelte";
  import CeyrekGram from "./CeyrekGram.svelte";
  import BesiBirlik from "./BesiBirlik.svelte";
  let alisValue = "";
  let satisValue;
  let Visible = false;

  $: alis.set(alisValue);
  $: satis.set(satisValue);
  $: if (alisValue !== "") {
    Visible = true;
  }
</script>

<Styles />

<Row>
  <Col sm="2"><Input placeholder="Alış" bind:value="{alisValue}" /></Col>
</Row>

<div>
  <Row>
    <Col sm="2"><Input placeholder="Satış" bind:value="{satisValue}" /></Col>
  </Row>
</div>

<hr />

{#if Visible}
  <div transition:fade><EskiCeyrek /></div>
{/if}
{#if Visible}
  <div transition:fade><YeniCeyrek /></div>
{/if}
{#if Visible}
  <div transition:fade><Bilezik /></div>
{/if}
{#if Visible}
  <div transition:fade><AtaLira /></div>
{/if}
{#if Visible}
  <div transition:fade><ResatLira /></div>
{/if}
{#if Visible}
  <div transition:fade><BirGram /></div>
{/if}
{#if Visible}
  <div transition:fade><YarimGram /></div>
{/if}
{#if Visible}
  <div transition:fade><CeyrekGram /></div>
{/if}
{#if Visible}
  <div transition:fade><BesiBirlik /></div>
{/if}

<style>
  div {
    padding-top: 1em;
  }
</style>
